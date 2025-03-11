<script>
	import pkg from "mapbox-gl";
	const { Map, mapboxgl } = pkg;
	import "mapbox-gl/dist/mapbox-gl.css";
	import { onMount, onDestroy } from "svelte";
	const { value } = $props();

	let map = $state();
	let mapContainer;
	let lng = -122.46836;
	let lat = 37.75784;
	let zoom = 11.49;

	// lng = -122.46836;
	// lat = 37.75794;
	// zoom = 11.49;
	$inspect(value);
	$inspect(map);
	let initiateState = { lng, lat, zoom };
	$effect(() => {
		if (!map) return;
		if (value === 0) {
			map.flyTo({
				center: [initiateState.lng, initiateState.lat],
				zoom: initiateState.zoom,
				speed: 0.5,
				essential: true
			});
		}
		if (value === 1) {
			console.log("hi"),
				map.flyTo({
					center: [-120.46836, 30.75794],
					zoom: 3,
					speed: 0.5,
					essential: true
				});
		}
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
