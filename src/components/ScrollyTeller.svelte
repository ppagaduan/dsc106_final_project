<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { geoMercator } from "d3-geo";
  import Map from "./Map.svelte"
  import { onMount } from 'svelte';
  import Graph from './Graph.svelte';
  import Viz from './viz.svelte';
  import * as d3 from 'd3';
  import Button from './Button.svelte';

  let count, index, offset, progress;
  let width, height;
  let data = [];

  onMount(
    async() => {
      const res = await fetch('aids_cases_by_region.csv')
      const csv = await res.text();
      data = d3.csvParse(csv, d3.autoType)
    }
  )

  let geoJsonToFit = { // added
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
    <h2 class="subheading">
      Timeline
    </h2>
    <div class="row">

      <div class="column">
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
      </div>

      <div class="column">
        <p class = 'blurb'>
          HIV was discovered and AIDS became globally recognized by the World Health Organization.
        </p>
  
  
        <p class = 'blurb'>
          The AIDS epidemic became widespread in the U.S. 
        </p>
  
  
  
        <p class = 'blurb'>
          blah blah blah
        </p>
  
  
  
        <p class = 'blurb'>
          blah blah blah
        </p>

        <p class = 'blurb'>
          blah blah blah blah blabh lbah
        </p>

      </div>
    </div>
  </section>

  <section class = 'global_impact'>
    <h2 class = 'subheading'>
      Worldwide Reach: Mapping the Prevalence of HIV/AIDS
    </h2>
    <Map bind:geoJsonToFit {index}/> 
    <Graph {index} {width} {height} {projection} /> 
    <br> <br> <br> <br>  <br> <br> <br> <br> <br> <br> <br> <br> <br> <br> <br> <br> 
    <br> <br> <br> <br>  <br> <br> <br> <br> <br> <br> <br> <br> <br> <br> <br> <br>
    <br> <br> <br> 
    <p class = 'blurb'>
      This map is centered on Eswatini, formerly known as Swaziland, located in Southern Africa. It is almost entirely
    landlocked by South Africa, and is also bordered by Mozambique. Eswantini, along with other countries in Southern Africa,
    have some of the highest percentages of adult prevalence of HIV / AIDS in the country. To view other countries, use your cursor
    to zoom in and out of the map!
    </p> <br> <br> <br> <br> <br> <br> 
  </section>

  <section class = 'global_impact'>
    <h2 class = 'subheading'>
      Charting AIDS Prevalence Across Nations
    </h2>
    <h3>Use the slider to observe the change in global AIDS cases by year! </h3>
    <Viz/>
    <br>
    <br>
    <br>
    <br>
    <br>
    <p class = 'blurb'>
      insert analysis of global impact rates here
    </p>
  </section>

  <section class = 'global_impact'>
    <h2 class = 'subheading'>
      Risk Factors & Transmission
    </h2>
    <h3> Click a button below to learn about the different transmission methods and risk factors. </h3>
    <Button class="unprotected_sex" buttonText= "Unprotected Sex"> 
    </Button> <br><br>

    <Button class="drug_usage" buttonText = "Drug Usage">
    </Button> <br><br>

    <Button class="mother_to_child_transmission" buttonText = "Mother to Child Transmission">
    </Button> <br><br>

    <Button class="sti" buttonText = "Sexually Transmitted Infections">
    </Button>
    <br><br> ------------------------ <br>
    <h3> Click the button below to see how HIV transmits between people. </h3>

    <section class = 'blood'>
      <Button class='HIV' buttonText='HIV'> </Button>
    </section>

  </section>

  <section class = 'treatment_and_prevention'>  
    <h2 class = 'subheading'>
      Treatment and Prevention
    </h2>
  </section>

  <section class = 'call_to_action'>
    <h2 class = 'subheading'>
      How You Can Help <!-- resource links -->
    </h2>
  </section>

  <section>
    <h2 class="subheading">
      Reflection
    </h2>
    <h3 class = 'instructions'> 1. What have you done so far? <br>
      2. What will be the most challenging of your project to design and why?</h3>
    <p class = "blurb">
      So far, we have created the base template for the layout of our website. The ScrollyTeller is functional and is based off of
      Lab 7. Each section of our website will detail a different aspect of the AIDS epidemic that we want to communicate to the
      viewer, as represented through the headings in each section. We have also imported our interactive bar chart from Project 3 to
      this project, as it touches on the same topics and is helpful to describe the trends in AIDS cases throughout the years.
      Additionally, we've included a world map that is zoomable to one of the sections to further emphasize the global impact that AIDS
      has. <br> <br>
      The most challenging part of the project to design will be the timeline, in our opinion. We are attempting to have the decade
      years tween in through animation, as well as have the information associated with each year toggle in and out depending on how
      far down the page the viewer has scrolled. However, our current implemenation of these animations is not working and Lab 7 does not
      provide an adequate template that we can use for this process. But after the lectures this week about animation in data
      visualizations, we think that we can approach this issue with a new perspective and try to implement these animations 
      successfully. 
    </p>
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

  .column {
  float: left;
  width: 50%;
  }

  .instructions{
    text-align: left;
  }

  /* Clear floats after the columns */
  .row:after {
    content: "";
    display: table;
    clear: both;
  }

  .timeline{
    height: 150vh;
    font-family: 'Nunito', sans-serif;
  }

  .global_impact{
    height: 120vh;
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

  .blood {
    width: 100%;
    height: 60vh;
    position: relative;
    background-color: rgba(255, 0, 0, 0.2);
  }
</style>
