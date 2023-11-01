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
		'D.O.T.S Projector',
		'Ghost Writing',
		'EMF Level 5',
		'Ghost Orb',
		'Ultraviolet',
		'Freezing Temperatures',
		'Spirit Box'
	];

	onMount(async () => {
		let resp = await fetch(`${BASE_URL}/breeds`);
		breeds = await resp.json();
		console.log(breeds);

		let breed;
		let breedImg;

		for (let i = 0; i < cats.length; i++) {
			breed = breeds[cats[i].index];
			cats[i].name = breed.name;
			resp = await fetch(`${BASE_URL}/images/search?breed_ids=${breed.id}&api_key=${key}`);
			breedImg = await resp.json();
			console.log(breedImg);
			cats[i].img = breedImg[0].url;
		}
	});

	function switchCat() {
		catIndex++;
		catIndex %= cats.length;
	}
</script>

<section class="gallery">
	<h2>{cats[catIndex].name}</h2>
	<div class="card">
		<div class="cardImg" title={cats[catIndex].name}>
			<div class="filmGrain" />
			<div class="darken" />
			<img src={cats[catIndex].img} alt="picture of {cats[catIndex].name}" />
		</div>
		<h3>Evidence</h3>
		<p>{evidence[cats[catIndex].evidence[0]]}</p>
		<p>{evidence[cats[catIndex].evidence[1]]}</p>
		<p>{evidence[cats[catIndex].evidence[2]]}</p>
	</div>
    <button on:click={switchCat} style="position:absolute;top:0px">next</button>
</section>

<style>
	section.gallery {
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		flex-wrap: wrap;
		width: 100%;
		height: 100vh;
	}

	.card {
		height: 200px;
		width: 400px;
		padding: 5px;
		display: flex;
		flex-direction: column;
		flex-wrap: wrap;
		border: solid black;
	}

	.cardImg {
		width: 711px;
		height: 400px;
	}

	.cardImg img {
		width: inherit;
		height: inherit;
		object-fit: stretch;
	}
</style>
