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

		let frameNo = 1;
		for (let i = 0; i < cats.length; i++) {
			breed = breeds[cats[i].index];
			cats[i].name = breed.name;
			resp = await fetch(`${BASE_URL}/images/search?breed_ids=${breed.id}&api_key=${key}`);
			breedImg = await resp.json();
			console.log(breedImg);
			cats[i].img = breedImg[0].url;
			cats[i].frame = `../img/taped_photo_frame_${frameNo}.png`
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
		catIndex %= cats.length;
	}
</script>

<section class="guide">
	<div class="filmGrain" />
	<div class="darken" />
	<div class="journal">
		<div class="photo" style="rotate:{cats[catIndex].rotate}deg;">
			<div class="tape" style="background-image:url({cats[catIndex].frame})"/>
			<div class="img" style="background-image:url({cats[catIndex].img})">
				<div class="filmGrain" />
				<div class="darken" />
			</div>
		</div>
		<h2>Evidence</h2>
		<p>{evidence[cats[catIndex].evidence[0]]}</p>
		<p>{evidence[cats[catIndex].evidence[1]]}</p>
		<p>{evidence[cats[catIndex].evidence[2]]}</p>
	</div>

	
	<button on:click={nextCat} style="position:absolute;top:0px;">next</button>
	<button on:click={prevCat} style="position:absolute;top:30px;">prev</button>
</section>

<style>
	section.guide {
		background-image: url(../img/inside_ridgeview.jpg);
		background-size: contain;
		background-position: center;
		background-repeat: no-repeat;
		display: flex;
		justify-content: center;
		align-items: center;
		width: 100%;
		height: 1080px;
	}
	
	div.journal {
		box-sizing: border-box;
		z-index: 6;
		background-image: url(../img/journal.png);
		background-size: contain;
		background-position: center;
		background-repeat: no-repeat;
		width: 1339px;
		height: 979px;
		padding: 50px 75px;
		border: dotted green;
	}

	.photo {
		width: 576px;
		height: 324px;
		display: flex;
		justify-content: center;
		align-items: center;
		rotate: 5deg;
	}

	.photo > .tape {
		position: absolute;
		width: inherit;
		height: inherit;
		background-size: contain;
		background-repeat: no-repeat;
		background-position: center;
		z-index: 5;
	}

	.photo > .img {
		position: relative;
		width: 78%;
		height: 78%;
		background-size: cover;
		background-position: center;
	}
</style>
