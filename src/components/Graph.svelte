<script>
    import { fly, draw } from "svelte/transition";
    import { tweened } from "svelte/motion";
    import { cubicOut, cubicInOut } from "svelte/easing";

    export let index, width, height, projection;

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

    $: tweenedData = years.map((city, i) => ({
        x: $tweenedX[i],
        y: $tweenedY[i],
        properties: city.properties,
    }));

    $: {
        if (index === 1) {
        tweenedX.set(years.map((city) => width / 2));
        tweenedY.set(years.map((city, i) => height / 2 + i * 20));
        }

        if (index > 1) {
        tweenedX.set(
            cities.features.map((city) => projection(city.geometry.coordinates)[0])
        );
        tweenedY.set(
            cities.features.map((city) => projection(city.geometry.coordinates)[1])
        );
        }
    }
</script>

