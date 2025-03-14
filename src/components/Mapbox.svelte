<script>
	import pkg from "mapbox-gl";
	const { Map, mapboxgl } = pkg;
	import "mapbox-gl/dist/mapbox-gl.css";
	import { onMount, onDestroy } from "svelte";
	const { value } = $props();

	let map = $state();
	let mapContainer;
	let lng = -122.36125;
	let lat = 37.8664;
	let zoom = 13.93;
	//[-122.36125, 37.86640]
	// lng = -122.46836;
	// lat = 37.75794;
	// zoom = 11.49;
	$inspect(value);
	$inspect(map);
	let initiateState = { lng, lat, zoom };
	$effect(() => {
		if (!map) return;
		if (value === 0) {
			//inside the bay
			map.flyTo({
				center: [initiateState.lng, initiateState.lat],
				zoom: initiateState.zoom,
				speed: 0.5,
				essential: false //defines whether or not the map is essential for the story. mainly toggled for people who may choose to turn off motion sickness blurs
			});
		}
		if (value === 1) {
			//SF Map
			console.log("hi"),
				map.flyTo({
					center: [-122.45676, 37.76061],
					zoom: 11.71,
					speed: 0.5,
					essential: false
				});
		}
		if (value >= 2 && value <= 6) {
			console.log("hi"),
				map.flyTo({
					center: [-122.46836, 37.75794],
					zoom: 11.49,
					speed: 0.5,
					essential: false
				});
		} ///values to then be the steps here.
	});

	onMount(() => {
		map = new Map({
			container: mapContainer,
			accessToken: import.meta.env.VITE_MAPBOX_ACCESS_TOKEN,
			style: "mapbox://styles/alariosjz/cm80g039d02dk01qo9u3f4j70",
			center: [initiateState.lng, initiateState.lat],
			zoom: initiateState.zoom,
			interactive: false
		});
	});

	onDestroy(() => {
		if (map) {
			map.remove();
		}
	});
</script>

<div class="map" bind:this={mapContainer}></div>

<style>
	.map {
		position: absolute;

		height: 100%;
		width: 100%;
	}
</style>
