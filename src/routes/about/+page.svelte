
<script>
/*
  About page that describes the game and suggestor
*/
  let suggestor = true;

  let suggestorActive = () => {
    suggestor = true;
  };

  let gameActive = () => {
    suggestor = false;
  };
</script>

<section class="container">
  <section class="tabs">
    <button on:click={suggestorActive} class:activeButton={suggestor == true}
      >About The Suggestor</button
    >
    <button on:click={gameActive} class:activeButton={suggestor == false}
      >About The Game</button
    >
  </section>

  <section class="content">
    <div id="suggestor" class:active={suggestor == true}>
      <h2>Suggestor</h2>
      <p>
        Our game suggestor is a tool designed to help you find the perfect game
        to play next! simply use the filters to search for a game that suits
        what you're looking for, and watch the results update in front of you
        eyes!
      </p>
      <a href="suggestor">Click here to find a game!</a>
    </div>

    <div id="game" class:active={suggestor == false}>
      <h2>The Game</h2>
      <p>
        Gamedle is a guessing game, similar to games like wordle, but instead of
        guessing a word, you're guessing a video game! <br /><br />Each time you
        guess incorrectly, you will recieve another clue until you can guess
        correctly! <br /><br />once you've won, simply press the reset button to
        start a new game! all of your scores will be tracked underneath the game
        area.
      </p>
      <a href="game">Click here to play!</a>
    </div>
  </section>
</section>

<style>
  div {
    display: none;
  }
  .active {
    display: contents;
  }
  .content {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .content div {
    align-self: center;
  }
  .content div p {
    max-width: 30em;
    align-self: center;
    padding-bottom: 1em;
  }
  .content div a {
    align-self: center;
  }
  h2 {
    text-align: center;
  }
  .container {
    padding-top: 5vh;
    display: flex;
    flex-direction: column;
    width: fit-content;
    height: fit-content;
    margin: 0 auto;
  }
  section {
    align-self: center;
  }
  button {
    background-color: var(--highlightText);
    margin-right: 5px;
    margin-bottom: 5px;
    margin-top: 5px;
    height: 3em;
    width: 7em;
  }
  button:hover {
    background-color: var(--secondaryHighlight);
    color: white;
    transform: scale(1.2);
    transition-duration: 500ms;
  }
  .activeButton {
    background-color: var(--secondaryHighlight);
    color: white;
  }
  a {
    color: var(--highlightText);
    text-decoration: underline;
    text-decoration-color: var(--highlightText);
  }
  a:visited {
    color: var(--highlightText);
    text-decoration: underline;
    text-decoration-color: var(--highlightText);
  }
  a:hover {
    color: var(--mainText);
  }
</style>
