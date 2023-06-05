<script>
  /*
    This page has the 'wordle like' guessing game
  */
  import { data } from "../../../gamedata.js";
  import { onMount } from "svelte";

  let previousGames = [];
  let previousGuesses = [];

  onMount(async () => {
    let guesses = localStorage.getItem("guesses");
    let games = localStorage.getItem("games");
    if (guesses) {
      previousGuesses = [...guesses.split(",")];
      previousGames = [...games?.split(",")];
    }
  });
  data.sort((a, b) => {
    return a.Title.localeCompare(b.Title);
  });

  let random = Math.floor(Math.random() * 100); //generates a random number to represent a game from the dataset
  let answer = data[random];
  while ( previousGames.includes(answer.Title) && previousGames.length < 100)
  {
    //Rerolls the answer if it is one that has already been played
    console.log(answer.Title);
    random = Math.floor(Math.random() * 100);
    answer = data[random];
  }

  let nameHint = answer.Title.charAt(0).toString();
  for (let i = 1; i < answer.Title.length; i++)
  {
    //Creates a hangman style clue
    {answer.Title.charAt(i) != " " ? (nameHint += "_") : (nameHint += " ");}
  }
  let clues = [
    `Release Year: ${answer.ReleaseYear.toString()}`,
    `Genre: ${answer.Genre}`,
    `Developer: ${answer.Developer}`,
    `Platforms ${answer.Platforms}`,
    nameHint,
  ];

  let givenClues = [`Release Year: ${answer.ReleaseYear.toString()}`]; //The year is the first clue given to the player
  let guesses = 0;
  let guess = data[0].Title;
  let correctGuess = false;

  let changeGuess = () => {
    guess = document.querySelector("input")?.value;
  };
  let reset = () =>
    //resets the game by resetting the random answer, cluse, guesses and count.
    {
      document.querySelector("input").value = "";
      guesses = 0;
      random = Math.floor(Math.random() * 100);
      answer = data[random];

      while (previousGames.includes(answer.Title) && previousGames.length < 100)
      {
        //Rerolls the answer if it is one that has already been played
        console.log(answer.Title);
        random = Math.floor(Math.random() * 100);
        answer = data[random];
      }

      nameHint = answer.Title.charAt(0).toString();
      for (let i = 1; i < answer.Title.length; i++)
      { 
        {answer.Title.charAt(i) != " " ? (nameHint += "_") : (nameHint += " ");} 
      }

      clues = [
        `Release Year: ${answer.ReleaseYear.toString()}`,
        `Genre: ${answer.Genre}`,
        `Developer: ${answer.Developer}`,
        `Platforms ${answer.Platforms}`,
        nameHint,
      ];

      correctGuess = false;
      givenClues = [`Release Year: ${answer.ReleaseYear.toString()}`];
    };
  let checkAnswer = () => {
    document.querySelector("input").value = "";

    if (!correctGuess) {
      //If the game is not over
      guesses++;
      if (guesses < clues.length) {
        givenClues = [];
        for (let i = 0; i <= guesses; i++) {
          givenClues[i] = clues[i];
        }
      }

      if (guess === answer.Title) {
        correctGuess = true; //Stops the player from guessing again
        givenClues = clues;
        previousGuesses = [...previousGuesses, guesses];
        previousGames = [...previousGames, answer.Title];

        //stores previous scores to local storage, so they persist if the page is reloaded
        localStorage.setItem("games", previousGames);
        localStorage.setItem("guesses", previousGuesses);
      }
    }
  };

let clearScores = () => {
  previousGames = [];
  previousGuesses = [];
  localStorage.clear();
}
</script>

<section class="container">
  <section class="clues">
    <h2>Hints:</h2>
    {#each givenClues as clue}
      <p>{clue}</p>
    {/each}
  </section>
  <section class="answerSelector">
    <label for="selectAnser">Select Answer:</label>
    <input
      type="text"
      list="gamesList"
      name="answer"
      id="selectAnswer"
      on:change={changeGuess}
    />
    <datalist id="gamesList">
      {#each data as game}
        <option value={game.Title}>{game.Title}</option>
      {/each}
    </datalist>
  </section>
  <section class="buttons">
    <button class="checkButton" on:click={checkAnswer}> Check </button>
    <button class="resetButton" on:click={reset}> Reset </button>
  </section>
  <p>
    {correctGuess === true
      ? `Correct! You guessed it in ${guesses} guesses`
      : `Incorrect! ${guesses} guesses.`}
  </p>
  <br />
  <section>
    <h2>Previous Scores:</h2>
    <div class="scores">
      {#each previousGames as game, index}
        <div class="eachScore">
          <p>Game: {game}</p>
          <p>Guesses: {previousGuesses[index]}</p>
        </div>
      {/each}
    </div>
    <button class="clearButton" on:click={clearScores}>Clear all scores</button>
  </section>
</section>


<style>
  p {
    display: flex;
    justify-content: center;
  }
  section {
    padding: 10px;
  }
  .clues {
    padding: 0px 10px;
    justify-content: center;
    height: 9lh;
  }
  .answerSelector {
    display: flex;
    justify-content: center;
  }
  label {
    padding-right: 10px;
  }
  h2 {
    display: flex;
    justify-content: center;
    color: var(--highlightText);
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
  .clearButton {
    font-size: 12px;
    background-color: rgb(204, 55, 55);
    width: fit-content;
  }
  .clearButton:hover {
    background-color: rgb(255, 0, 0);
    border-color: rgb(255, 0, 0);
  }
  .scores {
    max-width: 900px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  .eachScore {
    min-width: 250px;
    margin: 10px;
  }
</style>
