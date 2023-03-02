<script>
    import "../style.css";
    import Navigation from '$lib/navigation.svelte';
    import Footer from '$lib/footer.svelte';
</script>

<Navigation />
<br/>
<slot /> <!-- page specific content -->
<br/>
<Footer />