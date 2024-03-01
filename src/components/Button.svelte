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
                message.set("Insert cool information about topic here :)");
            } else if (buttonProps.class.includes('drug_usage')) {
                message.set("insert info here :D")
            } else if (buttonProps.class.includes('mother_to_child_transmission')){
                message.set("yay more opportunities to learn stuff")
            } else if (buttonProps.class.includes('sti')){
                message.set("replace this box with more info & visuals later")
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