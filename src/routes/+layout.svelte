<script>
  import "../style.css";
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
</script>

<Header />
<main>
  <slot />
  <!-- page specific content -->
</main>
<Footer />

<style>
  main {
    min-height: 85vh;
    color: var(--bodyText);
    background-color: var(--lightColour);
    background-size: 100%;
    margin: 0px;
  }
  main{
    padding-top: 10vh;
  }
</style>
