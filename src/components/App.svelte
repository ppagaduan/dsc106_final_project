<script>
  import * as d3 from 'd3';
  import { onMount } from "svelte";

  // mapboxgl.accessToken = "pk.eyJ1IjoicHBhZ2FkdWFuIiwiYSI6ImNsdDY2cDgyNjA4cWIybHBkNHpnaHg1YjYifQ.JC-taM_C1H3Ch8uJ2p_Hzw";
</script>

<main>
  <h1 class='title'>Journey Through Time</h1>
  <h2 class='subtitle'> An Interactive Exploration of AIDS History</h2>
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
    font-size: 50;
    font-weight: 500;
    line-height: 2;
    background-color: #f16a73;
    color: black
  }

  .subtitle{
    font-size: 10;
    font-weight: 500;
    line-height: 2;
    background-color: #f16a73;
    color: black;
  }
</style>