<script>
  import "../style.css";
  import Header from "$lib/header.svelte";
  import Footer from "$lib/footer.svelte";

//Fetch for getting "gaming" images from unsplash

  // let imagesArray = [];

  // const BASE_URL = "https://api.unsplash.com/";
  // fetch(
  //   `${BASE_URL}/search/photos/?client_id=skDU48Yd4CUD6X2AaBJDlof39G4ykmRrVtvUKKLG2Ks&query=gaming`
  // )
  //   .then((res) => res.json())
  //   .then((data) => {
  //     data.results.forEach((element) => {
  //       imagesArray.push(element.urls.small);
  //     });
  //   });
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
  }
  div {
    width: 50vw;
    min-height: 85vh;
    color: var(--bodyText);
    background-color: var(--lightColour);
    background-size: 100%;
    margin: auto;
    padding-top: 10vh;
  }
  slot{
  animation-name: slide-in;
    animation-duration: 1s;
  }
  @keyframes slide-in{
    from{
      transform: translateY(-200%);
    }
    to{
      transfrom: translateY(0%);
    }
  }
</style>
