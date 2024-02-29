<script>
	import mapboxgl from 'mapbox-gl';
	import 'mapbox-gl/dist/mapbox-gl.css';
	import { onMount, onDestroy } from "svelte";
	mapboxgl.accessToken = "pk.eyJ1IjoiaHRhbTg4IiwiYSI6ImNsc2d2M2xrMzB0YXAycnBncWNwMWlkc3gifQ._-vNYE1-qImQWrRbu76uUw";

	let mapContainer;

	onMount(() => {
	const world_map = new mapboxgl.Map({
		container: mapContainer,
		style: "mapbox://styles/mapbox/light-v11", 
		center: [0, 0], 
		zoom: 13, // starting zoom level
		minZoom: 12,
		maxZoom: 15,
        height: 400,
        width: 400,
	});
	
	});
	
	

    // world_map.on("load", () => {
	// 	world_map.addSource("world_map", {
	// 		type: "geojson",
	// 		data: "https://raw.githubusercontent.com/ppagaduan/dsc106_final_project/main/static/world_map.geo.json",
	// 	});
	// 	world_map.addLayer({
	// 		id: "world_map",
	// 		type: "fill",
	// 		source: "world_map",
	// 		paint: {
    //             "fill-color": "#BEE5B0",
    //             "fill-opacity": 0.5,
	// 		},
	// 	});
	// });

</script>

<div class="map-wrap">
	<div class="map" bind:this={mapContainer} />
</div>

<style>
	.map {
	position: absolute;
	width: 100%;
	height: 100%;
}
</style>