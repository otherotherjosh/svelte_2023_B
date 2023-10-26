<script>
    import { onMount } from "svelte";

    const key = "live_vG0dMaOCuDHFd0eSo0eGuC4J6QcX02uCLeMwnDr6DXqQxeVA6ATgx9NwJX5z59g4";
    const BASE_URL = "https://api.thecatapi.com/v1";
    let cats = [];
    let breeds = {
        "java" : [0, 3, 4],
    };
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
        let resp = await fetch(`${BASE_URL}/images/search?limit=10&api_key=${key}`);
        cats = await resp.json();
        console.log(cats);
    });
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