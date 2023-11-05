<script>
	import { onMount } from 'svelte';

	const key = 'live_vG0dMaOCuDHFd0eSo0eGuC4J6QcX02uCLeMwnDr6DXqQxeVA6ATgx9NwJX5z59g4';
	const BASE_URL = 'https://api.thecatapi.com/v1';
	let cats = [
		{ index: 35, evidence: [0, 3, 4] }, // Banshee - java
		{ index: 40, evidence: [1, 4, 5] }, // Demon - mcoo
		{ index: 66, evidence: [0, 1, 6] }, // Deogen - ycho
		{ index: 45, evidence: [3, 4, 5] }, // Hantu - norw
		{ index: 61, evidence: [0, 2, 5] }, // Oni - sphy
		{ index: 29, evidence: [1, 3, 5] }, // Revenant - emau
		{ index: 0, evidence: [1, 2, 5] }, // Shade - abys
		{ index: 4, evidence: [1, 2, 6] }, // Spirit - asho
		{ index: 15, evidence: [4, 5, 6] }, // The Mimic - bure
		{ index: 56, evidence: [2, 5, 6] }, // The Twins - siam
		{ index: 54, evidence: [0, 3, 6] } // Yokai - sfol
	];

	let breeds = [];
	let catIndex = 0;

	const evidence = [
		'C.A.T.S Projector',
		'Cat Writing',
		'EMF Level 5',
		'Cat Orb',
		'Ultraviolet',
		'Freezing Temperatures',
		'Litter Box'
	];

	onMount(async () => {
		let resp = await fetch(`${BASE_URL}/breeds`);
		breeds = await resp.json();
		console.log(breeds);

		let breed;
		let breedImg;

		let frameNo = 1;
		for (let i = 0; i < cats.length; i++) {
			breed = breeds[cats[i].index];
			cats[i].name = breed.name;
			resp = await fetch(`${BASE_URL}/images/search?breed_ids=${breed.id}&api_key=${key}`);
			breedImg = await resp.json();
			cats[i].img = breedImg[0].url;
			cats[i].frame = `../img/taped_photo_frame_${frameNo}.png`;
			cats[i].rotate = Math.floor(Math.random() * 11) - 5;
			frameNo++;
			if (frameNo > 4) frameNo = 1;
		}
	});

	function nextCat() {
		catIndex++;
		catIndex %= cats.length;
	}

	function prevCat() {
		catIndex--;
		if (catIndex < 0) catIndex = cats.length - 1;
		console.log(catIndex);
	}
</script>

<section class="guide">
	<div class="filmGrain" />
	<div class="darken" />
	<div class="journal">
		<div class="page">
			<h1>{cats[catIndex].name}</h1>
			<div class="photo" style="rotate:{cats[catIndex].rotate}deg;">
				<p>loading image</p>
				<div class="tape" style="background-image:url({cats[catIndex].frame})" />
				<div class="filmGrain" />
				<div class="img" style="background-image:url({cats[catIndex].img})" />
			</div>
			<h2>Evidence</h2>
			<h3>{evidence[cats[catIndex].evidence[0]]}</h3>
			<h3>{evidence[cats[catIndex].evidence[1]]}</h3>
			<h3>{evidence[cats[catIndex].evidence[2]]}</h3>
		</div>
		<div class="page" />
		<button on:click={prevCat} style="left: 0px;" />
		<button on:click={nextCat} style="right: 0px;" />
	</div>
</section>
