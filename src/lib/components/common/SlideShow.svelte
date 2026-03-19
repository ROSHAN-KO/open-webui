<script lang="ts">
	import { WEBUI_BASE_URL } from '$lib/constants';
	import { onMount } from 'svelte';

	export let imageUrls = [
		`${WEBUI_BASE_URL}/assets/images/doflamingo.jpg`,
		`${WEBUI_BASE_URL}/assets/images/Luffy_vs_Lucchi.jpg`,
		`${WEBUI_BASE_URL}/assets/images/sanji_water7.jpg`,
		`${WEBUI_BASE_URL}/assets/images/Whitebeard.jpg`
	];
	export let duration = 5000;
	let selectedImageIdx = 0;

	onMount(() => {
		setInterval(() => {
			// Removed the "- 1" so it loops through all 4 images perfectly
			selectedImageIdx = (selectedImageIdx + 1) % imageUrls.length;
		}, duration);
	});
</script>

{#each imageUrls as imageUrl, idx (idx)}
	<div
		class="image w-full h-full absolute top-0 left-0 bg-cover bg-center transition-opacity duration-1000"
		style="opacity: {selectedImageIdx === idx ? 1 : 0}; background-image: url('{imageUrl}')"
	></div>
{/each}

<style>
	.image {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-size: cover;
		background-position: center;
		transition: opacity 1s ease-in-out;
		opacity: 0;
	}
</style>
