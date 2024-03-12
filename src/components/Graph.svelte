<script>
    import { fly, draw } from "svelte/transition";
    import { tweened } from "svelte/motion";
    import { cubicOut, cubicInOut } from "svelte/easing";

    export let index, width, height;

    let years = {
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
          "decade": "1980s" 
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
          "decade": "1990s"
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
          "decade": "2000s"
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
          "decade": "2010s"
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
          "decade": "2020s"
        }
      }
    ]
  }

    let info = {
    "type": "FeatureCollection",
    "features": [
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            50
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "AIDS is globally recognized by the" 
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            75
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "World Health Organization & the"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            100
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": " Center for Disease Control."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            150
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "The U.S. Congress allocates nearly "
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            175
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "$190 million for AIDS research."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            50
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact" : "First antiretroviral (ARV) drug approved "
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            75
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "by U.S. FDA."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            125
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "AIDS becomes first disease debated on "
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            150
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "floor of United Nations (UN) General "
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            175
          ]
        },
        "properties": {
          "decade": "1980s",
          "fact": "Assembly."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            250
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "American Disabilities Act of 1990 to"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            275
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "combat anti-AIDS sentiment &"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            300
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "prohibit discrimination."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            350
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "Number of new AIDS cases diagnosed"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            375
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "in U.S. declines for first time in history"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            400
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "of the epidemic."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            250
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "Brazil begins national ARV distribution,"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            275
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "the first developing country to do so."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            325
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "International Council of AIDS "
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            350
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "Service Organizations forms as global"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            375
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "network of non-governmental &"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            400
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "community-based organizations."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            475
          ]
        },
        "properties": {
          "decade": "2000s",
          "fact": "President Clinton announces"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            500
          ]
        },
        "properties": {
          "decade": "2000s",
          "fact": "Millennium Vaccine Initiative, creating"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            525
          ]
        },
        "properties": {
          "decade": "2000s",
          "fact": "incentives for development &"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            550
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "distribution of vaccines against HIV, TB"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            575
          ]
        },
        "properties": {
          "decade": "2000s",
          "fact": "& malaria."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            475
          ]
        },
        "properties": {
          "decade": "2000s",
          "fact": "U.S. National Security Council and UN"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            500
          ]
        },
        "properties": {
          "decade": "1990s",
          "fact": "Security Council each declare HIV/AIDS"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            525
          ]
        },
        "properties": {
          "decade": "2000s",
          "fact": "a security threat."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            650
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "Obama Administration releases first"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            675
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "comprehensive National HIV/AIDS"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            700
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "Strategy for U.S."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            750
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "White House announces updated"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            775
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "National HIV/AIDS Strategy for U.S."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            650
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "WHO validates Cuba’s elimination of"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            675
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "mother-to-child transmission of HIV"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            700
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "and syphilis."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            750
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "U.N. and partners announce pricing"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            775
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "agreement to accelerate the availability"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            800
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "of first affordable, generic, single-pill"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            825
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "HIV treatment in low-income countries."
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            900
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "Anthony Fauci, MD, director of the"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            925
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "National Institute of Allergy & Infectious"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            950
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "Diseases, compares lessons learned"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            975
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "in the AIDS epidemic & the COVID-19"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            1000
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "pandemic during a presentation for the"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            15,
            1025
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "Center for AIDS Research."
        }
      },     
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            900
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "FDA updates its blood donor eligibility"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            925
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "guidance, ending longstanding"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            950
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "discriminatory policies that excluded gay"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            975
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "& bisexual people from donating blood"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            1000
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "while maintaining appropriate"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Point",
          "coordinates": [
            500,
            1025
          ]
        },
        "properties": {
          "decade": "2010s",
          "fact": "safeguards to protect recipients of blood."
        }
      },
    ]
  }
    const tweenOptions = {
    delay: 0,
    duration: 1000,
    easing: cubicOut,
    };

    const tweenedYearsX = tweened(
        years.features.map((decade) => (decade.geometry.coordinates)[0]),
        tweenOptions
    );

    const tweenedYearsY = tweened(
        years.features.map((decade) => (decade.geometry.coordinates)[1]),
        tweenOptions
    );

    const tweenedInfoX = tweened(
        info.features.map((fact) => (fact.geometry.coordinates)[0]),
        tweenOptions

    );

    const tweenedInfoY = tweened(
        info.features.map((fact) => (fact.geometry.coordinates)[1]),
        tweenOptions

    );

  $: tweenedYears = years.features.map((decade, i) => ({
    x: $tweenedYearsX[i],
    y: $tweenedYearsY[i],
    properties: decade.properties,
  }));

  $: tweenedFacts = info.features.map((fact, i) => ({
    x: $tweenedInfoX[i],
    y: $tweenedInfoY[i],
    properties: fact.properties,
  }));

  $: {
    if (index === 1) {
      tweenedYearsX.set(years.features.map((decade) => width / 2));
      tweenedYearsY.set(years.features.map((decade, i) => height / 2 + i * 20));

      tweenedInfoX.set(info.features.map((fact) => width / 2));
      tweenedInfoY.set(info.features.map((fact, i) => height / 2 + i * 20));
    }

    if (index > 2) {
      tweenedYearsX.set(
        years.features.map((decade) => (decade.geometry.coordinates)[0])
      );
      tweenedYearsY.set(
        years.features.map((decade) => (decade.geometry.coordinates)[1])
      );

      tweenedInfoX.set(
        info.features.map((fact) => (fact.geometry.coordinates)[0])
      );
      tweenedInfoY.set(
        info.features.map((fact) => (fact.geometry.coordinates)[1])
      );
    }
  }
</script>

<svg class="graph">
{#if index > 2}
    {#each tweenedYears as decade, i}
      {#if decade.x && decade.y}
        <text
          x={decade.x}
          y={decade.y}
          font-size = 60px
          font-color= "red"
          id={decade.properties.name}
          in:fly={{ x: -300, duration: 200 * i }}
          out:fly={{ x: -300, duration: 200 * i }}
          >{decade.properties.decade}
        </text>
      {/if}
    {/each}

    {#each tweenedFacts as info, i}
    {#if info.x && info.y}
      <text
        x={info.x}
        y={info.y}
        font-size = 14px
        text-anchor = 'center'
        id={info.properties.name}
        in:fly={{ x: -300, duration: 200 * i }}
        out:fly={{ x: -300, duration: 200 * i }}
        >{info.properties.fact}
      </text>
    {/if}
  {/each}
{/if}
</svg>

<style>
    .graph {
      width: 100%;
      height: 120vh; /* check problem when setting width */
      position: center;
      outline: red solid 7px;
    }
</style>