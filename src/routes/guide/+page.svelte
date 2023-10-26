<script>
    import { onMount } from "svelte";

    const key = "live_vG0dMaOCuDHFd0eSo0eGuC4J6QcX02uCLeMwnDr6DXqQxeVA6ATgx9NwJX5z59g4";
    const BASE_URL = "https://api.thecatapi.com/v1";
    let cats = [];
    let breeds = [
        {id: "java", evidence: [0, 3, 4], img: ""},
        {id: "mcoo", evidence: [1, 4, 5], img: ""},
        {id: "ycho", evidence: [0, 1, 6], img: ""}
    ];
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
        breeds.forEach(breed => addBreedData(breed))
    });

    async function addBreedData(breed) {
        let resp = await fetch(`${BASE_URL}/images/search?breed_ids=${breed.id}&api_key=${key}`);
        let data = await resp.json();
        breed.img = data[0].url;
        console.log(breed);
        cats.push(breed);
        cats = cats;
    }
</script>

<section class="gallery">
    {#each cats as cat}
        <div>
            <div class="imgBackground" style=background-image:url({cat.img})></div>
            <h2>{cat.id}</h2>
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