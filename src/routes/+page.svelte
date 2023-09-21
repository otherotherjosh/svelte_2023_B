<script>
    const BASE_URL = `https://api.unsplash.com`;
    const CLIENT_ID = `z40TIIyaq-YDho1wKR7UKenm1vj6ZA6nio7GVDJ-dLE`;

    let cats = [];

    fetch(`${BASE_URL}/search/photos?query=cats&client_id=${CLIENT_ID}`)
    .then(res => res.json())
    .then(data => {
        cats = data.results
    })
</script>

<style>
    .gallery{
        display: grid;
        grid-template: repeat(1fr, 3) / repeat(100px, 3);
    }

    .gallery div{
        /* make the cats visible somehow */
    }
</style>

<div class="gallery">
    {#each cats as cat}
        <img src={cat.urls.regular} alt="cat"/>
    {/each}
</div>
