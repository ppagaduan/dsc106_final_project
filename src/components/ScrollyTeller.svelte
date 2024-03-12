<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import { geoMercator } from "d3-geo";
  import Map from "./Map.svelte"
  import { onMount } from 'svelte';
  import Graph from './Graph.svelte';
  import Viz from './viz.svelte';
  import * as d3 from 'd3';
  import Button from './Button.svelte';
  import Stage from './Stage.svelte';

  let count, index, offset, progress;
  let width, height;
  let data = [];
  onMount(
    async() => {
      const res = await fetch('HIV_demographic_data.csv')
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

      <img src = 'https://medlineplus.gov/images/HIV.png' alt = ''>

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
        <span class="bullet">>></span> HIV is theorized to have originally spread from chimpanzees to humans. Based on numerous studies, researchers believe 
        the initial form of HIV came from a type of chimpanzee in Central Africa, as far back as the 1800s.  <br>
        <span class="bullet">>></span> The chimpanzee form of the HIV virus was called simian immunodeficiency virus. Scientists believe humans acquired this 
        virus when humans hunted chimpanzees for their meat, and became ill when they became in contact with the chimpanzees' 
        infected blood. <br>
        <span class="bullet">>></span> Over time, HIV spread through Africa, and eventually other parts of the world. HIV has been recorded in the United States 
        since the mid to late 1970s. According to the CDC (Center for Disease Control), in 2006, about 56,000 people in the United
        States had acquired AIDS, a late stage of the HIV infection. <br>
      </p>
  </section>

  <section class = 'symptoms_and_stages'> 
    <p class = 'subheading'>
      The Symptoms
    </p>

    <!-- <Stage {index} {width} {height}/>  -->
    <p class="symptoms">
      <span class="bullet">>></span> fever <br>
      <span class="bullet">>></span> night sweats <br>
      <span class="bullet">>></span> mouth ulcers <br>
      <span class="bullet">>></span> sore throat <br>
      <span class="bullet">>></span> swollen lymph nodes <br>
      <span class="bullet">>></span> chills <br>
      <span class="bullet">>></span> fatigue <br>
      <span class="bullet">>></span> rash <br>
      <span class="bullet">>></span> muscle aches <br>
    </p>

    <p class="subheading">
      Stages of HIV
    </p>
    <!-- image -->
    <img src = "https://hivinfo.nih.gov/sites/default/files/fact_sheets_data/images/hiv-progression.jpg" alt = '' width = 600>
    <!-- stage 1 -->
    <p class='subheading3'>
      STAGE 1: ACUTE HIV INFECTION
    </p>
    <p class = 'blurb'>
      <span class="bullet">>></span> Develops 2-4 weeks after infection with HIV<br>
      <span class="bullet">>></span> Flu-like symptoms: fever, headache, rash <br>
      <span class="bullet">>></span> HIV multiplies rapidly and destroys CD4 T lymphocytes, which fight infections <br>
      <span class="bullet">>></span> High levels of HIV are present in the blood
    </p>
    <!-- stage 2 -->
    <p class='subheading3'>
      STAGE 2: CHRONIC HIV INFECTION
    </p>
    <p class = 'blurb'>
      <span class="bullet">>></span> Also known as asymptotic HIV infection or clinical latency <br>
      <span class="bullet">>></span> People may not have symptoms related to HIV <br>
      <span class="bullet">>></span> HIV continues to multiply in the bloodstream but at a lower rate <br>
      <span class="bullet">>></span> Without antiretroviral treatment, people could remain in this stage for as long as a decade
    </p>
    <!-- stage 3-->
    <p class='subheading3'>
      STAGE 3: AIDS
    </p>
    <p class = 'blurb'>
      <span class="bullet">>></span> The most severe and final stage of the HIV infection <br>
      <span class="bullet">>></span> The body is too weak to fight off infections or infection-related cancer <br>
      <span class="bullet">>></span> The person afflicted has a CD4 count of less than 200 cells / mm^3 <br>
      <span class="bullet">>></span> People are highly contagious and can quickly transmit HIV to others <br>
      <span class="bullet">>></span> People with AIDS usually survive about 3 more years
    </p>
    
  </section>

  <section class = 'stats'>
    <p class = 'subheading'>
      The Stats
    </p> <br>

    <p class='instructions'> Let's visualize global HIV statistics. Each square will represent 1 million people. 
      Click the '1' below to begin. Continue clicking the '1' until the simulation has ended.</p>
    <Button class = 'population' buttonText = 1> </Button>
  </section>

  <section class = 'timeline'> 
    <h2 class="subheading">
      Timeline
    </h2>
    <Graph {index} {width} {height}/> 
  </section>

  <section class = 'global_impact'>
    <h2 class = 'subheading'>
      Worldwide Reach: Mapping the Prevalence of HIV/AIDS
    </h2>
    <Map bind:geoJsonToFit {index}/> 
    <br>
    <p class = 'blurb'>
      This map is centered on Eswatini, formerly known as Swaziland, located in Southern Africa. It is almost entirely
    landlocked by South Africa, and is also bordered by Mozambique. Eswantini, along with other countries in Southern Africa,
    have some of the highest percentages of adult prevalence of HIV / AIDS in the country. To view other countries, use your cursor
    to zoom in and out of the map!
    </p>
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
      Note: Some countries appear to have multiple columns within the same year. This is because some countries received multiple records
      of data that year. <br>
      insert analysis of global impact rates here
    </p>
  </section>

  <section class = 'risk_factors_and_transmission'>
    <h2 class = 'subheading'>
      Risk Factors & Transmission
    </h2>
    <p class = 'instructions', style="text-align:center"> Click a button below to learn about the different transmission methods and risk factors. </p>
    <Button class="unprotected_sex" buttonText= "Unprotected Sex"> 
    </Button> <br><br>

    <Button class="drug_usage" buttonText = "Drug Usage">
    </Button> <br><br>

    <Button class="mother_to_child_transmission" buttonText = "Mother to Child Transmission">
    </Button> <br><br>

    <Button class="sti" buttonText = "Sexually Transmitted Infections">
    </Button>
    <br><br> ------------------------ <br>
    <p class = 'instructions'> Click the green button below, labelled 'HIV', below to visualize the rate of HIV replication. Continue
      clicking the 'HIV' button until the simulation has ended.</p>

    <div class = 'blood'>
      <Button class='HIV' buttonText='HIV'> </Button>
    </div>

  </section>

  <section class = 'call_to_action'>
    <h2 class = 'subheading'>
      Let's Save Lives Together <!-- resource links -->
    </h2>
    <h3 class = 'instructions'> HIV is still a persisting issue. According to UNAIDS, in 2022, about 39 million people globally
      were afflicted with HIV. Of these people, 1.3 million were diagnosed with HIV that year, which is a 38% decline in new infections
      since 2010 and a 59% decline since HIV was most prevalent in 1995. Click the links below to explore how you can help combat HIV and AIDS.
    </h3>

    <!-- donate -->
    <h2 class = 'subheading2'> Donate</h2>
    <a href = 'https://www.unaids.org/en/donate'> 
      <Button buttonText = 'UNAIDS' class = 'donate'> </Button>
    </a>
    <a href = 'https://aidsunited.org/donate/'> 
      <Button buttonText = "AIDS United" class = 'donate'> </Button>
    </a>
    <a href = 'https://www.amfar.org'> 
      <Button buttonText = 'The Foundation for AIDS Research (amfAR)' class = 'donate'> </Button>
    </a>

    <!-- volunteer -->
    <h2 class = 'subheading2'> Volunteer </h2>
    <a href = 'http://beingalivesd.com'> 
      <Button buttonText = 'Being Alive' class = 'volunteer'> </Button>
    </a>
    <a href = 'https://christiesplace.org/volunteer/'> 
      <Button buttonText = "Christie's Place" class = 'volunteer'> </Button>
    </a>
    <a href = 'https://sdvlp.org/hiv-aids-law/'> 
      <Button buttonText = 'San Diego Volunteer Lawyer Program' class = 'volunteer'> </Button>
    </a>

    <!-- learn more links -->
    <h2 class = 'subheading2'> Learn More </h2>
    <a href = 'https://www.cdc.gov/hiv/basics/whatishiv.html#:~:text=What%20is%20HIV%3F,they%20have%20it%20for%20life.'> 
      <Button buttonText = 'Centers for Disease Control & Prevention (CDC)' class = 'learn_more'> </Button>
    </a>
    <a href = 'https://www.hiv.gov/hiv-basics/overview/about-hiv-and-aids/what-are-hiv-and-aids'> 
      <Button buttonText = 'HIV.gov' class = 'learn_more'> </Button>
    </a>
    <a href = 'https://www.who.int/news-room/fact-sheets/detail/hiv-aids'> 
      <Button buttonText = 'World Health Organization (WHO)' class = 'learn_more'> </Button>
    </a>
  </section>

  <section class = 'references'>
    <h2 class = 'subheading'>
      References
    </h2>
    <a href = https://docs.idmod.org/projects/emod-hiv/en/2.20_a/hiv-disease-overview.html>
      <p class = 'blurb'>
        Bill & Melinda Gates Foundation. (n.d.). HIV disease overview. HIV disease overview - HIV Model documentation.
      </p>
    </a>

    <a href = https://www.cdc.gov/hiv/basics/hiv-transmission/substance-use.html>
      <p class = 'blurb'>
        Centers for Disease Control and Prevention. (2021, April 21). HIV and substance use. Centers for Disease Control and Prevention. 
      </p>
    </a>

    <a href = https://www.cdc.gov/hiv/basics/whatishiv.html>
      <p class = 'blurb'>
        Centers for Disease Control and Prevention. (2022, June 30). About HIV/AIDS. Centers for Disease Control and Prevention. 
      </p>
    </a>
    
    <a href = https://www.unaids.org/en/resources/fact-sheet>
      <p class = 'blurb'>
        Global HIV & AIDS statistics - fact sheet. UNAIDS. (n.d.). 
      </p>
    </a>

    <a href = https://www.hiv.gov/hiv-basics/overview/history/hiv-and-aids-timeline>
      <p class = 'blurb'>
        HIV.gov. (n.d.). Timeline of the HIV and AIDS epidemic. HIV.gov. 
      </p>
    </a>

    <a href = https://www.lehigh.edu/~jas0/V16.html> 
      <p class = 'blurb'>
        Lehigh University. (n.d.). BIOS 353
      </p>
    </a>

    <a href = https://medlineplus.gov/images/HIV_share.png>
      <p class = 'blurb'>
        MedlinePlus. (n.d.). Image of HIV.
      </p>
    </a>

    <a href = https://www.kff.org/global-health-policy/timeline/global-hivaids-timeline/ >
      <p class = 'blurb'>
        Global HIV/AIDS timeline. KFF. 
      </p>
    </a>

    <a href = https://hivinfo.nih.gov/understanding-hiv/fact-sheets/stages-hiv-infection>
      <p class = 'blurb'>
        U.S. Department of Health and Human Services. (n.d.). The stages of HIV infection. National Institutes of Health.
      </p>
    </a>
    
    <a href = https://www.nichd.nih.gov/health/topics/hiv/conditioninfo/factors>
      <p class = 'blurb'>
        U.S. Department of Health and Human Services. (n.d.). What factors make HIV more likely?. Eunice Kennedy Shriver National Institute of Child Health and Human Development.
      </p>
    </a>

    <a href = https://www.census.gov/data-tools/demo/hiv/#/records>
      <p class = 'blurb'>
        United States Census Bureau. (n.d.). International Programs - HIV Surveillance Data base. United States Census Bureau.
      </p>
    </a>

    <a href = https://www.who.int/news-room/fact-sheets/detail/hiv-aids>
      <p class = 'blurb'>
        World Health Organization. (n.d.). HIV and AIDS. World Health Organization.
      </p>
    </a>
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
    background-color: rgba(244, 126, 85, 0.2);
  }

  .foreground {
    width: 57%;
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

  .subheading2{
    font-family: 'Nunito', sans-serif;
    font-size: 2em;
    font-weight: 150;
    line-height: 1;
    color: red
  }

  .subheading3{
    font-family: 'Nunito', sans-serif;
    text-align: left;
    font-size: 2em;
    font-weight: 150;
    line-height: 1;
    color: #F47e55;
  }

  .intro{
    height: 125vh;
  }

  .blurb{
    font-family: 'Nunito', sans-serif;
    text-align: left;
    font-size: 1em;
    font-weight: 200;
    line-height: 2;
  }  

  .symptoms{
    font-family: 'Nunito', sans-serif;
    transform: translateX(325px);
    text-align: left;
  }

  .instructions{
    font-family: 'Nunito', sans-serif;
    text-align: center;
    font-weight: bold;
  }

  .symptoms_and_stages{
    height: 200vh
  }

  .timeline{
    height: 150vh;
    font-family: 'Nunito', sans-serif;
  }

  .global_impact{
    height: 130vh;
    font-family: 'Nunito', sans-serif;
  }

  .risk_factors_and_transmission {
    height: 175vh;
  }

  .blood {
    width: 100%;
    height: 60vh;
    background-color: rgba(255, 0, 0, 0.2);

    outline: brown 3px;
    text-align: center;
    max-width: 800px; /* adjust at will */
  }

  .bullet {
    color: #F47e55;
    font-weight: bold;
  }

  .call_to_action{
    height: 100vh;
  }

  .references {
    height: 125vh;
  }

  section {
    height: 80vh;
    background-color: rgba(98, 204, 245, 0.2); /* 20% opaque */
    /* color: white; */
    outline: brown 3px;
    text-align: center;
    max-width: 800px; 
    color: black;
    padding: 1em;
    margin: 0 0 2em 0;
  }
</style>
