<script>
  import * as d3 from 'd3';
  // import ScrollyTeller from './ScrollyTeller.svelte';
  import { onMount } from "svelte";
</script>

<main>
  <h1 class='title'>HIV</h1>
  
  <div class = 'intro'>
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
  </div>


</main>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap');

  :root {
    --color-bg: #000000;
    --color-outline: #c2c2c2;
    --color-shadow: hsl(0, 0%, 0%, 0.1);
    --color-text: #000000;
    --color-bg-1: hsla(0, 0%, 0%, 0.2);
    --color-shadow-1: hsl(0, 0%, 96%);
  }

  *,
  *::before,
  *::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  main {
    text-align: center;
    font-family: 'Nunito', sans-serif;
    font-weight: 300;
    line-height: 2;
    font-size: 24px;
    color: var(--color-text);
  }

  .title{
    font-size: 4em;
    font-weight: 500;
    line-height: 2;
    background-color: #F4F0E8;
    color: #D6221D
  }

  .subheading{
    font-size: 2em;
    font-weight: 400;
    line-height: 2;
    color: #D6221D
  }

  .blurb{
    text-align: left;
    font-size: 1em;
    font-weight: 200;
    line-height: 2;
  }
</style>
