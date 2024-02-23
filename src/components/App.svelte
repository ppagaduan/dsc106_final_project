<script>
  import * as d3 from 'd3';
  // import ScrollyTeller from './ScrollyTeller.svelte';
  import { onMount } from "svelte";
</script>

<main>
  <h1 class='title'>HIV</h1>

  <p>Write your HTML here</p>
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
    font-size: 2em;
    font-weight: 300;
    line-height: 2;
    background-color: #F4F0E8;
    color: #D6221D
  }
</style>
