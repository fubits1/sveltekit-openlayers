<script>
	import { onMount } from 'svelte';
	import Map from 'ol/Map';
	import View from 'ol/View';
	import TileLayer from 'ol/layer/Tile';
	import XYZ from 'ol/source/XYZ';

	let map;
	let mapContainer;
	let isLoaded = false;

	$: isLoaded && map.getView().animate({ zoom: zoomLvl, duration: 600 });

	let zoomLvl = 2;
	onMount(() => {
		map = new Map({
			target: mapContainer, // 'map' works as well
			layers: [
				new TileLayer({
					source: new XYZ({
						url: 'https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png'
					})
				})
			],
			view: new View({
				center: [0, 0],
				zoom: zoomLvl
			})
		});

		isLoaded = true;
	});
</script>

<h1>OpenLayers</h1>
<input type="number" bind:value={zoomLvl} />
<div id="map" bind:this={mapContainer} />

<style>
	#map {
		width: 100vw;
		height: 80vh;
	}
</style>
