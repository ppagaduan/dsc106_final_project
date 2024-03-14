<script>
	import mapboxgl from "mapbox-gl";
	import { onMount } from "svelte";

	export let index;
  
	mapboxgl.accessToken =
	  "pk.eyJ1IjoiaHRhbTg4IiwiYSI6ImNsc2d2M2xrMzB0YXAycnBncWNwMWlkc3gifQ._-vNYE1-qImQWrRbu76uUw";
  

//connect HIV_demgraphic_data.csv to map 

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
  
	  map.on('load', () => {
      hideLabelLayers();
      updateBounds();
      map.on('zoom', updateBounds);
      map.on('drag', updateBounds);
      map.on('move', updateBounds);

      map.addSource('hiv_map', {
        type: 'geojson',
        data: 'https://raw.githubusercontent.com/htam88/dsc106_final_project_forked/main/static/map_data.geo.json',
      });

      map.loadImage(
        'https://docs.mapbox.com/mapbox-gl-js/assets/cat.png',
        (error, image) => {
          if (error) throw error;

          // Add the image to the map style.
          map.addImage('cat', image);

          map.addLayer({
            id: 'hiv_map',
            type: 'symbol',
            source: 'hiv_map',
            layout: {
              // Example of using an icon
              'icon-image': 'cat', // Use a predefined Mapbox icon or your custom icon
              // Example of adding text label
              'text-field': '{propertyName}', // Replace 'propertyName' with the field name from your GeoJSON properties
              'text-size': 12,
            },
          });
        },
      );
    });
	});
	
	function updateBounds() {
		const bounds = map.getBounds();

		if (geoJsonToFit.features.length === 0) {
			// Initialize the features array with two features if it's empty
			geoJsonToFit.features = [
				{
					type: 'Feature',
					geometry: {
						type: 'Point',
						coordinates: [bounds._ne.lng, bounds._ne.lat]
					}
				},
				{
					type: 'Feature',
					geometry: {
						type: 'Point',
						coordinates: [bounds._sw.lng, bounds._sw.lat]
					}
				}
			];
		} else {
			// If features already exist, just update their coordinates
			geoJsonToFit.features[0].geometry.coordinates = [bounds._ne.lng, bounds._ne.lat];
			geoJsonToFit.features[1].geometry.coordinates = [bounds._sw.lng, bounds._sw.lat];
		}
	}
  
	let isVisible = true;
  
  $: if (index === 4) {
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
	  width: 100%;
	  height: 80vh;
	  position: center;

	  opacity: 0;
	  visibility: hidden;
	  transition: opacity 2s, visibility 2s;
	  outline: red solid 7px;
	}
  
	.map.visible {
	  opacity: 1;
	  visibility: visible;
	}
  </style>
  
  