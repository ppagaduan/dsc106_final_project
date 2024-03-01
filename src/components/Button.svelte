<script>
    import {writable} from 'svelte/store';
    export let buttonText;

    let buttonProps = {
    class:[$$restProps.class]
    }
    let message = writable("");
    let isMessageVisible = false;

    function handleClick(customMessage){
        if (isMessageVisible){
            message.set(""); // hide the message when you unclick
        } else {
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
                gonorrhoea and bacterial vaginosis")
            }
            
        } isMessageVisible = !isMessageVisible;
    }
</script>
    <button on:click = {handleClick(buttonText)}
            on:mouseover
            on:focus
            on:mouseenter
            on:mouseleave
        {...buttonProps}>
            <slot/>
        {buttonText || 'Button'}
    </button>

    {#if $message}
        <p>{$message}</p>
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
</style>