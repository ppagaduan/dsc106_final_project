<script>
    let buttonProps = {
    class:[$$restProps.class]
    }
</script>
    <button on:click
            on:mouseover
            on:focus
            on:mouseenter
            on:mouseleave
        {...buttonProps}>
            <slot/>
    </button>

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