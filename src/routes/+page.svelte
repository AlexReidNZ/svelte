<script>
  /*
    Home page
  */
  import NavCard from "../lib/navCard.svelte";

  let pages = ["about", "suggestor", "game"];
</script>

<section class="container">
  <h1>Welcome to Gamedle!</h1>
  <br />
  <p>
    See the about page to learn more, or if you already know what you're doing
    here, go straight to the game suggestor or play a game!
  </p>
  <section class="cards">
    {#each pages as page}
      <NavCard pageName={page} />
    {/each}
  </section>
</section>

<style>
  section {
    padding-top: 5vh;
    display: flex;
    flex-direction: column;
  }
  p, h1 {
    align-self: center;
  }
  h1 {
    color: var(--highlightText);
    margin: 0;
  }
  .cards {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
  }
</style>
