<script>
    import Header from '$lib/Components/Header.svelte';
    import Footer from '$lib/Components/Footer.svelte';
</script>

<svelte:head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Lilita+One&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="css/main.css"/>
</svelte:head>

<Header/>

<slot/>

<Footer/>