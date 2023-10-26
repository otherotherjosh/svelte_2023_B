<script>
    import { onMount } from "svelte";

    const key = "live_vG0dMaOCuDHFd0eSo0eGuC4J6QcX02uCLeMwnDr6DXqQxeVA6ATgx9NwJX5z59g4";
    const BASE_URL = "https://api.thecatapi.com/v1";
    let cats = [
        {index: 35, evidence: [0, 3, 4]},
        {index: 40, evidence: [1, 4, 5]},
        {index: 66, evidence: [0, 1, 6]}
    ];

    let breeds = [];

    const evidence = [
        "D.O.T.S Projector",
        "Ghost Writing",
        "EMF Level 5",
        "Ghost Orb",
        "Ultraviolet",
        "Freezing Temperatures",
        "Spirit Box"
    ];

    onMount( async () => {
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

    async function addBreedData(breed) {
        let resp = await fetch(`${BASE_URL}/images/search?breed_ids=${breed.id}&api_key=${key}`);
        let data = await resp.json();
        breed.img = data[0].url;
        console.log(breed);

        resp = await fetch(`${BASE_URL}/breeds/search?breed_ids=${breed.id}`);
        data = await resp.json();
        console.log(data);

        cats.push(breed);
        cats = cats;
    }
</script>

<section class="gallery">
    {#each cats as cat}
        <div>
            <div class="imgBackground" style=background-image:url({cat.img})></div>
            <h2>{cat.name}</h2>
            <h3>Evidence</h3>
            <p>{evidence[cat.evidence[0]]}</p>
            <p>{evidence[cat.evidence[1]]}</p>
            <p>{evidence[cat.evidence[2]]}</p>
        </div>
    {/each}
</section>

<style>
    section.gallery {
        display: flex;
        justify-content: space-evenly;
        flex-wrap: wrap;
        width: 100%;
    }

    section.gallery > div {
        width: 200px;
        height: 200px;
    }
</style>