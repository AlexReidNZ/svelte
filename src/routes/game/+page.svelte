<script>
  import { data } from "../../../gamedata.js";

  let random = Math.floor(Math.random() * 100); //generates a random number from 1-99
  let answer = data[random];

  let guess = data[0];

  let correctGuess = false;

  let guesses = 0;
  let previousGuesses = 0;

  let changeGuess = () =>
    //sets the value of the players guesses to the value in the input.
    {
      let temp = document.getElementById("selectAnswer")?.value;
      console.log(temp);
      guess = temp;
    };
  let reset = () =>
    //resets the game by resetting the random answers, guesses and count.
    {
      guesses = 0;
      random = Math.floor(Math.random() * 100);
      answer = data[random];
      correctGuess = false;
    };
  let checkAnswer = () => 
    //checks if the answer is correct
    {
      guesses++;
      if (guess === answer)
      {
        correctGuess = true;
      }
      console.log(guess);
      console.log(correctGuess);
  };
</script>

<h1>Game</h1>
<br>
<p>{answer.Title}</p>
<br>
<label for="selectAnser">Select Answer:</label>
<select name="answer" id="selectAnser" on:change={changeGuess}>
  {#each data as game}
    <option value={game}>{game.Title}</option>
  {/each}
</select>
<br>
<section class="buttons">
  <button class="checkButton" on:click={checkAnswer}>
    <!--checks if the answer is correct-->
    Check
  </button>
  <button class="resetButton" on:click={reset}>
    <!--lets player reset the game-->
    Reset
  </button>
</section>
<br />
<p>
  {correctGuess === true ? `Correct! You guessed it in ${guesses} guesses` : ""}
</p>

<style>
  h1 {
    font-size: 30px;
    font-style: italic;
    font-weight: normal;
    display: flex;
    justify-content: center;
    margin: 0px;
  }
  p {
    display: flex;
    justify-content: center;
  }
  .buttons {
    display: flex;
    justify-content: center;
  }
  button {
    display: flex;
    justify-content: center;
    margin: 10px;
    width: 80px;
  }
  .resetButton {
    background-color: rgb(204, 55, 55);
  }
  .resetButton:hover {
    background-color: rgb(255, 0, 0);
    border-color: rgb(255, 0, 0);
  }
  .checkButton {
    background-color: rgb(80, 136, 80);
  }
  .checkButton:hover {
    background-color: rgb(26, 204, 26);
    border-color: rgb(26, 204, 26);
  }
</style>
