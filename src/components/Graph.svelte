<script>
    import { fly, draw } from "svelte/transition";
    import { tweened } from "svelte/motion";
    import { cubicOut, cubicInOut } from "svelte/easing";

    export let index, width, height;

    let years = ['1980s', '1990s', '2000s', '2010s', '2020s']

    const tweenOptions = {
    delay: 0,
    duration: 1000,
    easing: cubicOut,
    };

    const tweenedX = tweened(
        0,
        tweenOptions
    );

    const tweenedY = tweened(
        height / 4,
        tweenOptions
    );

    $: tweenedData = years.map((years, i) => ({
        x: $tweenedX[i],
        y: $tweenedY[i],
        years,
    }));

    $: {
        if (index === 1) {
        tweenedX.set(years.map((years) => width / 2));
        tweenedY.set(years.map((years, i) => height / 2 + i * 20));
        }

        if (index > 1) {
        tweenedX.set(
            years.features.map((years) => width / 2)
        );
        }
    }
</script>

