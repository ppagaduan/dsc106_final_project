<script>
    import { fly, draw } from "svelte/transition";
    import { tweened } from "svelte/motion";
    import { cubicOut, cubicInOut } from "svelte/easing";

    export let index, width, height;

    let symptoms = {
    "type": "FeatureCollection",
    "features": [
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            290,
            125
          ]
        },
        "properties": {
          "symptom": ">> fever" 
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            290,
            325
          ]
        },
        "properties": {
          "sypmtom": ">> night sweats"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            290,
            537.5
          ]
        },
        "properties": {
          "symptom": ">> mouth ulcers"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            290,
            725
          ]
        },
        "properties": {
          "symptom": "sore throat"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            290,
            975
          ]
        },
        "properties": {
          "symptom": ">> swollen lymph nodes"
        }
      }
    ]
  }
    const tweenOptions = {
    delay: 0,
    duration: 1000,
    easing: cubicOut,
    };

    const tweenedSymptomX = tweened(
        symptoms.features.map((symptom) => (symptom.geometry.coordinates)[0]),
        tweenOptions
    );

    const tweenedSymptomY = tweened(
        symptoms.features.map((symptom) => (symptom.geometry.coordinates)[1]),
        tweenOptions
    );

  $: tweenedSymptoms = symptoms.features.map((symptom, i) => ({
    x: $tweenedSymptomX[i],
    y: $tweenedSymptomY[i],
    properties: symptom.properties,
  }));

  $: {
    if (index === 0) {
      tweenedSymptomX.set(symptoms.features.map((symptom) => width / 2));
      tweenedSymptomY.set(symptoms.features.map((symptom, i) => height / 2 + i * 20));
    }

    if (index > 1) {
      tweenedSymptomX.set(
        sypmtoms.features.map((symptom) => (symptom.geometry.coordinates)[0])
      );
      tweenedSymptomY.set(
        symptoms.features.map((symptom) => (symptom.geometry.coordinates)[1])
      );
    }
  }
</script>

<svg class="graph">
{#if index > 1}
    {#each tweenedSymptoms as symptom, i}
      {#if symptom.x && symptom.y}
        <text
          x={symptom.x}
          y={symptom.y}
          font-size = 60px
          id={symptom.properties.symptom}
          in:fly={{ x: -300, duration: 200 * i }}
          out:fly={{ x: -300, duration: 200 * i }}
          >{symptoms.properties.symptom}
        </text>
      {/if}
    {/each}
{/if}
</svg>

<style>
    .graph {
      width: 100%;
      height: 50vh; /* check problem when setting width */
      position: center;
      outline: red solid 7px;
    }
</style>