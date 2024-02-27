<script>
	mapboxgl.accessToken = "pk.eyJ1IjoicHBhZ2FkdWFuIiwiYSI6ImNsc2pxMTltMjJ2bjcya3JreDd1dnFiMmMifQ.81ErEYIY2_oxdwbDSz2IDg";
	const map = new mapboxgl.Map({
		container: "map",
		style: "mapbox://styles/mapbox/light-v11", 
		center: [0, 0], 
		zoom: 13, // starting zoom level
		minZoom: 12,
		maxZoom: 15,
	});
    map.on("load", () => {
		map.addSource("world_map", {
			type: "geojson",
			data: "https://raw.githubusercontent.com/ppagaduan/dsc106_final_project/main/static/world_map.json",
		});
		map.addLayer({
			id: "world_map",
			type: "line",
			source: "world_map",
			paint: {
				"line-color": "#BEE5B0",
				"line-width": 3,
			},
		});
	});

</script>

