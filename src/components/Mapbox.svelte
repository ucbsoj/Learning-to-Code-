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
		if (value >= 2 && value <= 3) {
			//30 min
			console.log("hi"),
				map.flyTo({
					center: [-122.42924, 37.7387],
					zoom: 10.32,
					speed: 0.5,
					essential: false
				});
		}
		if (value >= 4 && value <= 5) {
			//1 hour
			console.log("hi"),
				map.flyTo({
					center: [-122.29326, 37.59667],
					zoom: 9.4,
					speed: 0.5,
					essential: false
				});
		}
		if (value >= 6 && value <= 7) {
			//begin the story
			console.log("hi"),
				map.flyTo({
					center: [-122.41608, 37.73089],
					zoom: 8.8,
					speed: 0.5,
					essential: false
				});
		}
		if (value >= 8 && value <= 9) {
			//capitola
			console.log("hi"),
				map.flyTo({
					center: [-121.96773, 36.97106],
					zoom: 13.26,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 10) {
			//grow capitola
			console.log("hi"),
				map.flyTo({
					center: [-122.07336, 37.18571],
					zoom: 9.58,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 11) {
			// cord entire
			console.log("hi"),
				map.flyTo({
					center: [-122.29592, 37.38058],
					zoom: 8.66,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 12) {
			//tracy
			console.log("hi"),
				map.flyTo({
					center: [-121.48742, 37.75276],
					zoom: 12.14,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 13) {
			//tracy mid
			console.log("hi"),
				map.flyTo({
					center: [-121.83676, 37.71429],
					zoom: 10.05,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 14) {
			// tracy end
			console.log("hi"),
				map.flyTo({
					center: [-122.01186, 37.69752],
					zoom: 9.63,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 15) {
			// los banos
			console.log("hi"),
				map.flyTo({
					center: [-120.8652, 37.06286],
					zoom: 12.72,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 16) {
			// los banos mid
			console.log("hi"),
				map.flyTo({
					center: [-121.11914, 37.30514],
					zoom: 9.31,
					speed: 0.5,
					essential: false
				});
		}
		if (value >= 17 && value <= 19) {
			// los banos end
			console.log("hi"),
				map.flyTo({
					center: [-121.90454, 37.5183],
					zoom: 8.23,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 20) {
			// orange
			console.log("hi"),
				map.flyTo({
					center: [-117.86084, 33.72782],
					zoom: 10.64,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 21) {
			// orange mid
			console.log("hi"),
				map.flyTo({
					center: [-121.41237, 35.65217],
					zoom: 6.39,
					speed: 0.5,
					essential: false
				});
		}
		if (value === 22) {
			// los medanos
			console.log("hi"),
				map.flyTo({
					center: [-122.2025, 37.86686],
					zoom: 9.93,
					speed: 0.5,
					essential: false
				});
		}
		if (value >= 23 && value <= 24) {
			// fishelson
			console.log("hi"),
				map.flyTo({
					center: [-122.26896, 37.64641],
					zoom: 8.68,
					speed: 0.5,
					essential: false
				});
		}

		// if (value >= 2 && value <= 6) {
		// 	console.log("hi"),
		// 		map.flyTo({
		// 			center: [-122.45676, 37.76061],
		// 			zoom: 11.71,
		// 			speed: 0.5,
		// 			essential: false
		// 		});
		///values to then be the steps here.
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
