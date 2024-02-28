<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { geoMercator } from "d3-geo";
  import Map from "./Map.svelte"
  import { onMount } from 'svelte';
  import Graph from './Graph.svelte';
  import Viz from './viz.svelte';

  let count, index, offset, progress;
  let width, height;

  let geoJsonToFit = {
    type: "FeatureCollection",
    features: [
      {
        type: "Feature",
        geometry: {
          type: "Point",
          coordinates: [1, 0],
        },
      },
      {
        type: "Feature",
        geometry: {
          type: "Point",
          coordinates: [0, 1],
        },
      },
    ],
  };

  $: projection = geoMercator().fitSize([width, height], geoJsonToFit);
</script>

<Scroller
top={0.0}
bottom={1}
threshold={0.5}
bind:count
bind:index
bind:offset
bind:progress
>
<div class="background" slot="background">

  <div class="progress-bars">
    <p>current section: <strong>{index + 1}/{count}</strong></p>
    <progress value={count ? (index + 1) / count : 0} />

    <p>offset in current section</p>
    <progress value={offset || 0} />

    <p>total progress</p>
    <progress value={progress || 0} />
  </div>
</div>

<div class="foreground" slot="foreground">

  <section class='intro'>

      <h2 class='subheading'>
        What is HIV?
      </h2>

      <p class = 'blurb'>
        Human immunodeficiency virus (HIV) is a virus that attacks the human immune system. There is currently no cure for HIV, 
        but with proper medical treatment, the effects of HIV can be controlled and those diagnosed with HIV can lead long, 
        healthy lives. Without proper treatment, HIV can lead to acquired immunodeficiency syndrome (AIDS). The most common ways that 
        HIV can be contracted is through sex with a partner with HIV, through perinatal transmission, and through the use of drug 
        injection equipment that has been contaminated by someone with HIV.
      </p>

      <h2 class='subheading'>
        The Start: How did HIV Originate?
      </h2>

      <p class='blurb'>
        >> HIV is theorized to have originally spread from chimpanzees to humans. Based on numerous studies, researchers believe 
        the initial form of HIV came from a type of chimpanzee in Central Africa, as far back as the 1800s.  <br>
        >> The chimpanzee form of the HIV virus was called simian immunodeficiency virus. Scientists believe humans acquired this 
        virus when humans hunted chimpanzees for their meat, and became ill when they became in contact with the chimpanzees' 
        infected blood. <br>
        >> Over time, HIV spread through Africa, and eventually other parts of the world. HIV has been recorded in the United States 
        since the mid to late 1970s. According to the CDC (Center for Disease Control), in 2006, about 56,000 people in the United
        States had acquired AIDS, a late stage of the HIV infection. <br>
      </p>
  </section>

  <section class = 'intro'> 
    <p class = 'subheading'>
      The Symptoms
    </p>

    <p class = 'subheading'>
      The Stages
    </p>

    <p class = 'subheading'>
      The Stats
      <!-- perhaps insert some static visualizations here -->
    </p>
  </section>

  <section class = 'timeline'> 
    <Graph {index} {width} {height} {projection} />

    <h2 class = 'subheading'>
      1980s
    </h2>

    <h2 class = 'subheading'>
      1990s
    </h2>

    <h2 class = 'subheading'>
      2000s
    </h2>

    <h2 class = 'subheading'>
      2010s
    </h2>

    <h2 class = 'subheading'>
      2020s
    </h2>
  </section>

  <section class = 'global_impact'>
    <h2 class = 'subheading'>
      Global Impact <!-- perhaps include an interactive or static map here?? -->
    </h2>
  	<div id = "map" ></div>
  </section>

  <section class = 'global_impact'>
    <h2 class = 'subheading'>
      Risk Factors & Transmission
    </h2>
    <Viz />
  </section>

  <section class = 'global_impact'>
    <h2 class = 'subheading'>
      Treatment & Prevention
    </h2>
  </section>

  <section class = 'call_to_action'>
    <h2 class = 'subheading'>
      How You Can Help <!-- resource links -->
    </h2>
  </section>

</div>
</Scroller>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap');
  .background {
    width: 100%;
    height: 100vh;
    position: relative;
    outline: red solid 3px;
  }

  .foreground {
    width: 50%;
    margin: 0 auto;
    height: auto;
    position: relative;
    outline: red solid 3px;
  }

  .progress-bars {
    position: absolute;
    background: rgba(241, 106, 115, 0.4) /*  20% opaque */;
    visibility: visible;
  }

  .subheading{
    font-family: 'Nunito', sans-serif;
    font-size: 2em;
    font-weight: 400;
    line-height: 2;
    color: red
  }

  .blurb{
    font-family: 'Nunito', sans-serif;
    text-align: left;
    font-size: 1em;
    font-weight: 200;
    line-height: 2;
  }

  .timeline{
    height: 150vh;
    font-family: 'Nunito', sans-serif;
  }

  section {
    height: 80vh;
    background-color: rgba(98, 204, 245, 0.2); /* 20% opaque */
    /* color: white; */
    outline: brown 3px;
    text-align: center;
    max-width: 800px; /* adjust at will */
    color: black;
    padding: 1em;
    margin: 0 0 2em 0;
  }
</style>
