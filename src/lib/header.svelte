<script>
  import Navigation from "./navigation.svelte";
</script>

<div>
  <header>Gamedle</header>
  <Navigation />
</div>

<style>
  header {
    height: 5vh;
    min-height: 40px;
    color: var(--highlightText);
    background-color: var(--darkColour);
    display: flex;
    justify-content: center;
    font-size: 40px;
  }
  div{
    position: fixed;
    width: 100vw;
  }
</style>
