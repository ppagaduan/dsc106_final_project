<script>
	mapboxgl.accessToken = "pk.eyJ1IjoicHBhZ2FkdWFuIiwiYSI6ImNsc2pxMTltMjJ2bjcya3JreDd1dnFiMmMifQ.81ErEYIY2_oxdwbDSz2IDg";
	const map = new mapboxgl.Map({
		container: "map",
		style: "mapbox://styles/mapbox/light-v11", 
		center: [0, 0], 
		zoom: 13, // starting zoom level
		minZoom: 12,
		maxZoom: 15,
        height: 400,
        width: 400,
	});
    map.on("load", () => {
		map.addSource("world_map", {
			type: "geojson",
			data: "https://raw.githubusercontent.com/ppagaduan/dsc106_final_project/main/static/world_map.geo.json",
		});
		map.addLayer({
			id: "world_map",
			type: "fill",
			source: "world_map",
			paint: {
                "fill-color": "#BEE5B0",
                "fill-opacity": 0.5,
			},
		});
	});

</script>