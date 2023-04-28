<script>
  import { data } from "../../../gamedata.js";

  let random = Math.floor(Math.random() * 100); //generates a random number from 1-99
  let answer = data[random];
  let clues = [
    answer.ReleaseYear.toString(),
    answer.Genre,
    answer.Developer,
    answer.Platforms,
  ];
  let givenClues = [answer.ReleaseYear.toString()];

  let guesses = 0;

  let guess = data[0].Title;

  let correctGuess = false;

  let changeGuess = () =>
    //sets the value of the players guesses to the value in the input.
    {
      let temp = document.getElementById("selectAnswer")?.value;
      guess = temp;
    };
  let reset = () =>
    //resets the game by resetting the random answers, guesses and count.
    {
      guesses = 0;
      random = Math.floor(Math.random() * 100);
      answer = data[random];
      clues = [
        answer.ReleaseYear.toString(),
        answer.Genre,
        answer.Developer,
        answer.Platforms,
      ];

      correctGuess = false;
      givenClues = [answer.ReleaseYear.toString()];
    };
  let checkAnswer = () =>
    //checks if the answer is correct
    {
      guesses++;
      if (guesses < clues.length) {
        givenClues = [];
        for (let i = 0; i <= guesses; i++) {
          givenClues[i] = clues[i];
        }
      }
      console.log(givenClues);

      if (guess === answer.Title) {
        correctGuess = true;
      }
    };
</script>

{#each givenClues as clue}
  <p>{clue}</p>
{/each}
<br />
<label for="selectAnser">Select Answer:</label>
<select name="answer" id="selectAnswer" on:change={changeGuess}>
  {#each data as game}
    <option value={game.Title}>{game.Title}</option>
  {/each}
</select>
<br />
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
  {correctGuess === true
    ? `Correct! You guessed it in ${guesses} guesses`
    : `Incorrect! ${guesses} guesses.`}
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
