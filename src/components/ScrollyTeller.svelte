<script>
    import Scroller from "@sveltejs/svelte-scroller";
  
    let count, index, offset, progress;
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

    </section>
    <section>This is the second section.</section>
    <section>This is the third section.</section>
  </div>
</Scroller>
  
  <style>
    .background {
      width: 100%;
      height: 100vh;
      position: relative;
      outline: green solid 3px;
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
      background: rgba(170, 51, 120, 0.2) /*  40% opaque */;
      visibility: visible;
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
  
    section {
      height: 80vh;
      background-color: rgba(0, 0, 0, 0.2); /* 20% opaque */
      /* color: white; */
      outline: magenta solid 3px;
      text-align: center;
      max-width: 800px; /* adjust at will */
      color: black;
      padding: 1em;
      margin: 0 0 2em 0;
    }
  </style>
  
