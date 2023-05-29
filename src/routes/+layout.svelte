<script>
  import "../style.css";
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";
</script>

<Header />
<main>
  <div>
    <slot />
    <!-- page specific content -->
  </div>
</main>
<Footer />

<style>
  main {
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
  slot {
    animation-name: slide-in;
    animation-duration: 1s;
  }
  @keyframes slide-in {
    from {
      transform: translateY(-200%);
    }
    to {
      transfrom: translateY(0%);
    }
  }
</style>
