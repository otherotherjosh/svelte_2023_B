<script>
    import Header from '$lib/Header.svelte';
    import Nav from '$lib/Nav.svelte';
    import Footer from '$lib/Footer.svelte';
</script>

<svelte:head>
    <link rel="stylesheet" href="css/main.css"/>
</svelte:head>

<Header/>
<Nav/>

<slot/>

<Footer/>