<script>
    import { onMount } from "svelte";

    const key = "live_vG0dMaOCuDHFd0eSo0eGuC4J6QcX02uCLeMwnDr6DXqQxeVA6ATgx9NwJX5z59g4";
    const BASE_URL = "https://api.thecatapi.com/v1";
    let cats = [];
    let breeds = [
        {name: "java", evidence: [0, 3, 4]},
        {name: "mcoo", evidence: [1, 4, 5]},
        {name: "ycho", evidence: [0, 1, 6]}
    ]
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
        breeds.foreach()
    });

    async function addBreed(breed) {
        let resp = await fetch(`${BASE_URL}/images/search?breed_ids={breed.id}?limit=1&api_key=${key}`);
        let data = await resp.json();
    }
</script>

<section class="gallery">
    {#each cats as cat}
        <div>
            <div class="imgBackground" style=background-image:url({cat.url})></div>
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