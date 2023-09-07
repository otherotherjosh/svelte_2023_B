<script>
    import Header from '$lib/Components/Header.svelte';
    import Footer from '$lib/Components/Footer.svelte';
</script>

<svelte:head>
    <link rel="stylesheet" href="css/main.css"/>
</svelte:head>

<Header/>

<slot/>

<Footer/>