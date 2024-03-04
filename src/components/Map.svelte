<script>
	import mapboxgl from "mapbox-gl";
	import { onMount } from "svelte";
	import Papa from 'papaparse';
	import { readable } from "svelte/store";

	export let index;
  
	mapboxgl.accessToken =
	  "pk.eyJ1IjoiaHRhbTg4IiwiYSI6ImNsc2d2M2xrMzB0YXAycnBncWNwMWlkc3gifQ._-vNYE1-qImQWrRbu76uUw";

	const aidsData = readable([], (set) => {
    fetch('../../static/HIV_demographic_data.csv')
      .then(response => response.text())
      .then(text => {
        const results = Papa.parse(text, { header: true }).data;
        set(results);
      });
  });
  
	let container;
	let map;
  
	let zoomLevel;
  	
	let geoJsonToFit = {
		'type': 'FeatureCollection',
		'features': []
	}
  
	function updateZoomLevel() {
	  const screenWidth = window.innerWidth;
	  zoomLevel = screenWidth <= 600 ? 4 : 5.85; // Adjust these values as needed
	}
  
	function handleResize() {
	  updateZoomLevel();
	  map.setZoom(zoomLevel);
	}
  
	onMount(() => {
	  updateZoomLevel();
	  map = new mapboxgl.Map({
		container,
		style: "mapbox://styles/mapbox/light-v11",
		center: [30, -30],
		zoom: zoomLevel,
		attributionControl: true, // removes attribution from the bottom of the map
	  });
  
	  window.addEventListener("resize", handleResize);
  
	  function hideLabelLayers() {
		const labelLayerIds = map
		  .getStyle()
		  .layers.filter(
			(layer) =>
			  layer.type === "symbol" && /label|text|place/.test(layer.id)
		  )
		  .map((layer) => layer.id);
  
		for (const layerId of labelLayerIds) {
		  map.setLayoutProperty(layerId, "visibility", "none");
		}
	  }
  
	  map.on("load", () => {
		hideLabelLayers();
		updateBounds();
		map.on("zoom", updateBounds);
		map.on("drag", updateBounds);
		map.on("move", updateBounds);
	  });
	});
	
	function updateBounds() {
	  const bounds = map.getBounds();
	  geoJsonToFit.features[0].geometry.coordinates = [
		bounds._ne.lng,
		bounds._ne.lat,
	  ];
	  geoJsonToFit.features[1].geometry.coordinates = [
		bounds._sw.lng,
		bounds._sw.lat,
	  ];
	}
  
	let isVisible = true;
  
  $: if (index === 3) {
	isVisible = true;
  } else {
	isVisible = false;
  }
  
  </script>
  
  <svelte:head>
	<link
	  rel="stylesheet"
	  href="https://api.mapbox.com/mapbox-gl-js/v2.14.0/mapbox-gl.css"
	/>
  </svelte:head>
  
  <div class="map" class:visible={isVisible} bind:this={container} />
  
  <style>
	.map {
	  width: 150%;
	  height: 80vh;
	  position: absolute;
	  left: -10vh;
	  opacity: 0;
	  visibility: hidden;
	  transition: opacity 2s, visibility 2s;
	  outline: blue solid 3px;
	}
  
	.map.visible {
	  opacity: 1;
	  visibility: visible;
	}
  </style>
  
  