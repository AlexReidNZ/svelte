<script>
  import "../style.css";
  import Header from "$lib/header.svelte";
  import Navigation from "$lib/navigation.svelte";
  import Footer from "$lib/footer.svelte";
</script>

<Header />
<Navigation />
<main>
  <slot />
  <!-- page specific content -->
</main>
<Footer />

<style>
  main {
    height: 87vh;
    color: var(--bodyText);
    background-color: var(--lightColour);
    background-size: 100%;
    margin: 0px;
  }
</style>
