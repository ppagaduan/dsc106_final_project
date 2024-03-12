<script>
    import {writable} from 'svelte/store';
    export let buttonText;

    let buttonProps = {
    class:[$$restProps.class]
    }
    let message = writable("");
    let isMessageVisible = false;
    let hivButtons = [];
    let popButtons = [];
    let replicationFactor = 3; 
    let isResetVisible = false;
    let count = 0;

    function handleClick(){
        if (buttonProps.class.includes("HIV")){ // simulation
            count = hivButtons.length * replicationFactor || 1;
            if (count < 2){
                hivButtons = Array.from({ length: count }, (_, i) => ({ label: "HIV " + (i + 1)}));
                message.set("HIV replicates in the bloodstream.");
            } else if (count < 5) {
                hivButtons = Array.from({ length: count }, (_, i) => ({ label: "HIV " + (i + 1)}));
                message.set("For an individual with HIV who is not currently receiving antiviral drug therapy, there are 10, 000\
                 virions per milliliter of blood. A virion is a functional virus that can affect living tissue; in our case, \
                 the virions are HIV.");
            } 
            else if (count < 10) {
                hivButtons = Array.from({ length: count }, (_, i) => ({ label: "HIV " + (i + 1)}));
                message.set("About 5,000 new virions per milliliter of blood are produced every day.");
            }else if (count < 30){
                hivButtons = Array.from({ length: count }, (_, i) => ({ label: "HIV " + (i + 1)}));
                message.set("Notice that in our simulation, the number of HIV viruses triples every time you click.\
                In real life, HIV's burst size, or number of virions produced per infected cell, can be between 1,000 and 3,000\
                virions. That means in our simulation, each additional HIV virion represents 1,000 virions in real life. This is \
                significantly faster than the burst size for influenza, also known as the flu, which is about 500-1,000 virions. ")
            }
            else if (count < 50) {
                hivButtons = Array.from({ length: count }, (_, i) => ({ label: "HIV " + (i + 1)}));
                message.set("HIV has a very high mutation rate, mutating at 3 x 10^(-5) nucleotide bases per cycle of replication.\
                On the other hand, he human genome typically mutates at a rate of 10^(-6) to 10^(-8) nucleotide bases per cycle of \
                replication.");
            } else if (count < 100){
                hivButtons = Array.from({ length: count }, (_, i) => ({ label: "HIV " + (i + 1)}));
                message.set("This means the virions produced every day can be very variable, making it harder for the human body to cope\
                with and for doctors to treat. As a result, HIV can spread very quickly if not treated early.");
            } else {
                message.set('The simulation has ended. Click the button below to play again.');
                isResetVisible = true;
            }

        } else if (buttonProps.class.includes("population")) { // stats demonstration
            if (count === 0) {
                count = 29
                popButtons = Array.from({ length: 29 }, (_, i) => ({label: i + 2, class: ''}));
                message.set('29.8 million people were accessing antiretroviral therapy to treat HIV in 2022.')
            } else if (count === 29) {
                count = 39
                popButtons = Array.from({ length: 38}, (_, i) => ({ label: i + 2, class: ''}));
                message.set('39 million people globally were living with HIV in 2022.');
            } else if (count === 39) {
                count = 40
                popButtons = Array.from({ length: 39}, (_, i) => ({ label: i + 2, class: ''}));
                message.set('Since the start of the HIV/AIDS epidemic, about 40.4 million people have died from AIDS-related illnesses.');
            } else if (count === 40) {
                count = 86
                popButtons = Array.from({ length: 85}, (_, i) => ({ label: i + 2, class: ''}));
                message.set('About 85.6 million people have become infected with HIV since the start of the epidemic.');
            } else {
                message.set('The simulation has ended. Click the button below to play again.');
                isResetVisible = true;
            }
        }
        
        else{
            if (isMessageVisible){
            message.set(""); // hide the message when you unclick
        } else { // risks & transmissions
                if (buttonProps.class.includes('unprotected_sex')){
                    message.set("People are at a higher risk of contracting HIV when they have anal or vaginal sex without a condom.\
                    This is fairly common among teenagers and young adults, age groups that tend to have higher rates of HIV compared\
                    to other Americans.");
                } else if (buttonProps.class.includes('drug_usage')) {
                    message.set("Studies have found the consumption of alcohol and/or drugs to also be associated with increased risks \
                    for HIV. Ingesting alcohol and using drugs can impair the user's judgement, causing them to partake in risky sexual \
                    behaviors, such as having unprotected sex or engaging in sexual activity with multiple partners. This can prompt \
                    a greater likelihood of contracting HIV. Sharing needles or syringes during drug injection can also increase risk\
                    since the needles may be contaminated. If a person currently has HIV, substance use can affect disease progression and\
                    adherence to HIV treatment (antiretroviral therapy), which can result in worse symptoms of the virus.")
                } else if (buttonProps.class.includes('mother_to_child_transmission')){
                    message.set("Babies can get HIV from their affected mothers before or during birth. Babies can also contract HIV \
                    from their mothers after birth through breastfeeding.")
                } else if (buttonProps.class.includes('sti')){
                    message.set("People with other sexually-transmitted infections (STIs), such as syphilis, herpes, chlamydia, \
                    gonorrhoea and bacterial vaginosis, are more susceptible to HIV.")
                }               
            }
        }
         isMessageVisible = !isMessageVisible;

    }

    function replay(){
            // reset everything to their initial state
            buttonProps = {
                class:[$$restProps.class]
            }
            message = writable("");
            hivButtons = [];
            popButtons = [];
            replicationFactor = 3; 
            isResetVisible = false;
            count = 0;
    }

</script>
    <button on:click = {handleClick}
            on:mouseover
            on:focus
            on:mouseenter
            on:mouseleave
        {...buttonProps}>
            <slot/>
        {buttonText || 'Button'}
    </button>

    <!-- HIV replication -->
    {#if buttonProps.class.includes('HIV')}
        {#each hivButtons as button, index}
            <button class='HIV' key={index}>{button.label}</button>
        {/each}

    {/if}

    <!-- stats visualization -->
    {#if buttonProps.class.includes('population')}
        {#each popButtons as button, index}
            <button class='population' key={index}>{button.label}</button>
        {/each}
    {/if}

    {#if $message}
        <p>{$message}</p>
    {/if}

    <!-- replay button -->
    {#if isResetVisible}
        <button on:click = {replay}>Replay ↻ </button>
    {/if}

<style>
    button{
        padding: 10px 20px;
        font-size: 16px;
    }
    .unprotected_sex{
        background-color: red;
        color:white;
    }
    .drug_usage {
        background-color: black;
        color:white;
    }
    .mother_to_child_transmission{
        background-color: lightblue;
        color: black;
    }
    .sti{
        background-color: yellow;
        color: black;
    }
    .HIV{
        background-color: lightgreen;
        color: black;
    }
    .hidden{
        display: None;
    }
    .learn_more{
        background-color: blue;
        color: white;
    }
    .volunteer{
        background-color: green;
        color: white;
    }
    .donate{
        background-color: lightblue;
        color: black;
    }
    .population{
        background-color: yellow;
        color: black;
    }
</style>