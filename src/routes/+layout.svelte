<script>
    import "../style.css";
    import Header from '$lib/header.svelte';
    import Navigation from '$lib/navigation.svelte';
    import Footer from '$lib/footer.svelte';
</script>

<Header />
<Navigation />
<slot /> <!-- page specific content -->
<Footer />