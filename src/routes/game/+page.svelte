<script>
  /*
    This page has the 'wordle like' guessing game
  */
  import { onMount } from "svelte";

  let previousGames = [];
  let previousGuesses = [];
  let games = [];
  let givenClues = [];
  let guesses = 0;
  let guess;
  let correctGuess;
  let clues = [];
  let answer;
  let random = 0;
  let nameHint;

  //Load the previous scores from local storage
  onMount(async () => {
    let guesses = localStorage.getItem("guesses");
    let games = localStorage.getItem("games");
    if (guesses) {
      previousGuesses = [...guesses.split(",")];
      previousGames = [...games?.split(",")];
    }
  });

  const url = "https://free-to-play-games-database.p.rapidapi.com/api/games"; //An api that contains data about free-to-play games
  const options = {
    method: "GET",
    headers: {
      "X-RapidAPI-Key": "bc956fa522msh60bbb4a61da609ep189239jsn473811898b52",
      "X-RapidAPI-Host": "free-to-play-games-database.p.rapidapi.com",
    },
  };

  fetch(url, options)
    .then((res) => res.json())
    .then((data) => {
      games = data;
      games.sort((a, b) => {
        return a.title.localeCompare(b.title);
      });

      random = Math.floor(Math.random() * games.length); //generates a random number to represent a game from the dataset
      answer = games[random];

      while (
        previousGames.includes(answer.title) &&
        previousGames.length < games.length
      ) {
        //Rerolls the answer if it is one that has already been played
        random = Math.floor(Math.random() * games.length);
        answer = games[random];
      }
      nameHint = answer.title.charAt(0).toString();
      for (let i = 1; i < answer.title.length; i++) {
        //Creates a hangman style clue
        {
          answer.title.charAt(i) != " " ? (nameHint += "_") : (nameHint += " ");
        }
      }

      answer.short_description = answer.short_description.replace(answer.title, nameHint); //Takes the games title out of its description

      clues = [
        `Genre: ${answer.genre}`,
        `Developer: ${answer.developer}`,
        `Release Date: ${answer.release_date}`,
        nameHint,
        `Description: ${answer.short_description}`,
      ];

      givenClues = [`Genre: ${answer.genre}`]; //The release date is the first clue given to the player
      guesses = 0;
      correctGuess = false;
    });

  let reset = () =>
    //resets the game by resetting the random answer, clues, guesses and count.
    {
      guess = "";
      guesses = 0;
      random = Math.floor(Math.random() * 100);
      answer = games[random];

      while (
        previousGames.includes(answer.title) &&
        previousGames.length < 100
      ) {
        //Rerolls the answer if it is one that has already been played
        random = Math.floor(Math.random() * 100);
        answer = games[random];
      }

      nameHint = answer.title.charAt(0).toString();
      for (let i = 1; i < answer.title.length; i++) {
        {
          answer.title.charAt(i) != " " ? (nameHint += "_") : (nameHint += " ");
        }
      }

      answer.short_description = answer.short_description.replace(answer.title, nameHint);

      clues = [
        `Genre: ${answer.genre}`,
        `Developer: ${answer.developer}`,
        `Release Date: ${answer.release_date}`,
        nameHint,
        `Description: ${answer.short_description}`,
      ];

      correctGuess = false;
      givenClues = [`Genre: ${answer.genre}`];
    };
  let checkAnswer = () => {
    if (!correctGuess) {
      //If the game is not over
      guesses++;
      if (guesses < clues.length) {
        givenClues = [];
        for (let i = 0; i <= guesses; i++) {
          givenClues[i] = clues[i];
        }
      }

      if (guess === answer.title) {
        correctGuess = true; //Stops the player from guessing again
        givenClues = clues;
        previousGuesses = [...previousGuesses, guesses];
        previousGames = [...previousGames, answer.title];

        //stores previous scores to local storage, so they persist if the page is reloaded
        localStorage.setItem("games", previousGames);
        localStorage.setItem("guesses", previousGuesses);
      }
    }
    guess = "";
  };

  let clearScores = () => {
    let clear = confirm("Are you sure you would like to clear your scores?");

    if (clear) {
      previousGames = [];
      previousGuesses = [];
      localStorage.clear();
    }
  };
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
      bind:value={guess}
    />
    <datalist id="gamesList">
      {#each games as game}
        <option value={game.title}>{game.title}</option>
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
  p, .answerSelector, button, .buttons, h2, .scores {
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
  label {
    padding-right: 10px;
  }
  h2 {
    color: var(--highlightText);
  }
  button {
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
    flex-wrap: wrap;
  }
  .eachScore {
    min-width: 250px;
    margin: 10px;
  }
</style>
