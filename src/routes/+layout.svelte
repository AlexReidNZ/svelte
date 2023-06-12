<script>
  import "../style.css";
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
</script>

<Header />
<section>
  <div>
    <slot /> <!-- page specific content -->
  </div>
</section>
<Footer />

<style>
  section {
    background-color: var(--lightColour);
    background-repeat: no-repeat;
    background-image: url("../images/Background.jpg");
    background-repeat: repeat;
  }
  div {
    min-width: fit-content;
    max-width: 50vw;
    min-height: 85vh;
    color: var(--bodyText);
    background-color: var(--lightColour);
    margin: auto;
    padding-top: 10vh;
    box-shadow: 10px;
  }
</style>
