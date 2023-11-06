<script>
	import { onMount } from 'svelte';
	import { cats } from "$lib/cats.js";
	import { evidence } from "$lib/evidence.js";
 
	const key = 'live_vG0dMaOCuDHFd0eSo0eGuC4J6QcX02uCLeMwnDr6DXqQxeVA6ATgx9NwJX5z59g4';
	const BASE_URL = 'https://api.thecatapi.com/v1';
	
	let breeds = [];
	let catIndex = 0;
	let rotateImages = [0, 0, 0, 0];

	onMount(async () => {
		randRotate();
		let resp = await fetch(`${BASE_URL}/breeds`);
		breeds = await resp.json();
		console.log(breeds);

		let breed;
		let breedImg;

		let frameNo = 1;
		for (let i = 0; i < cats.length; i++) {
			breed = breeds[cats[i].index];
			cats[i].name = breed.name;
			cats[i].description = breed.description;
			resp = await fetch(`${BASE_URL}/images/search?breed_ids=${breed.id}&api_key=${key}`);
			breedImg = await resp.json();
			cats[i].img = breedImg[0].url;
			cats[i].frame = `../img/taped_photo_frame_${frameNo}.png`;
			frameNo++;
			if (frameNo > 4) frameNo = 1;
		}
	});

	function nextCat() {
		catIndex++;
		catIndex %= cats.length;
		randRotate();
	}

	function prevCat() {
		catIndex--;
		if (catIndex < 0) catIndex = cats.length - 1;
		randRotate();
	}

	function randRotate() {
		let range = 5;
		let mult = range * 2 + 1;
		for (let i = 0; i < rotateImages.length; i++) {
			rotateImages[i] = Math.floor(Math.random() * mult) - range
		}
	}
</script>

<section class="guide">
	<div class="imgBackground" style="background-image:url(../img/inside_ridgeview.jpg);" />
	<div class="filmGrain" />
	<div class="journal">
		<div class="page">
			<h1>{cats[catIndex].name}</h1>
			<div class="photo" style="rotate:{rotateImages[3]}deg;">
				<p>loading image</p>
				<div class="tape" style="background-image:url({cats[catIndex].frame})" />
				<div class="filmGrain" />
				<div class="img" style="background-image:url({cats[catIndex].img})" />
			</div>
			<p>{cats[catIndex].description}</p>
		</div>
		<div class="page">
			<h2>Evidence</h2>
			{#each {length: 3} as _, i}
				<div class="evidence">
					<img src={evidence[cats[catIndex].evidence[i]].image} style="order:{(i + catIndex) % 2};rotate:{rotateImages[i]}deg;"/>
					<div class="text">
						<h3>{evidence[cats[catIndex].evidence[i]].name}</h3>
						<p>{evidence[cats[catIndex].evidence[i]].description}</p>
					</div>
				</div>
			{/each}
		</div>
		<button on:click={prevCat} style="left: 0px;" />
		<button on:click={nextCat} style="right: 0px;" />
	</div>
</section>
