<script>
  import { data } from "../../../gamedata.js";

  data.sort((a, b) => {
    //Sorts the data alphabetically by title
    return a.Title.localeCompare(b.Title);
  });

  let random = Math.floor(Math.random() * 100); //generates a random number from 0-99
  let answer = data[random];
  let nameHint = answer.Title.charAt(0).toString();
  for (let i = 1; i < answer.Title.length; i++) {
    //Creates a hangman style clue
    if (answer.Title.charAt(i) != " ") {
      nameHint = nameHint + "_";
    } else {
      nameHint = nameHint + " ";
    }
  }
  let clues = [
    `Release Year: ${answer.ReleaseYear.toString()}`,
    `Genre: ${answer.Genre}`,
    `Developer: ${answer.Developer}`,
    `Platforms ${answer.Platforms}`,
    nameHint,
  ];
  let givenClues = [`Release Year: ${answer.ReleaseYear.toString()}`]; //The year is the first given clue

  let guesses = 0;

  let guess = data[0].Title;

  let correctGuess = false;

  let previousGames = [""];
  previousGames = [];
  let previousGuesses = [0];
  previousGuesses = [];

  let changeGuess = () =>
    //sets the value of the players guesses to the value in the input.
    {
      let temp = document.getElementById("selectAnswer")?.value;
      guess = temp;
    };
  let reset = () =>
    //resets the game by resetting the random answer, cluse, guesses and count.
    {
      guesses = 0;
      random = Math.floor(Math.random() * 100);
      answer = data[random];
      nameHint = answer.Title.charAt(0).toString();
      for (let i = 1; i < answer.Title.length; i++) {
        if (answer.Title.charAt(i) != " ") {
          nameHint = nameHint + "_";
        } else {
          nameHint = nameHint + " ";
        }
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
  let checkAnswer = () =>
    //checks if the answer is correct
    {
      if (!correctGuess) {
        //If the game is not over
        guesses++;
        if (guesses < clues.length) {
          //gives the player the next clue if they don't already have them all
          givenClues = [];
          for (let i = 0; i <= guesses; i++) {
            givenClues[i] = clues[i];
          }
        }

        if (guess === answer.Title) {
          correctGuess = true;
          givenClues = clues; //shows the player all of the clues
          previousGuesses.push(guesses); //adds their score for this game to the array of past scores
          let tempGuesses = previousGuesses;
          previousGuesses = tempGuesses;
          previousGames.push(answer.Title); //adds the answer for this game to the array of past answers
          let tempTitles = previousGames;
          previousGames = tempTitles;
        }
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
    <select name="answer" id="selectAnswer" on:change={changeGuess}>
      {#each data as game}
        <option value={game.Title}>{game.Title}</option>
      {/each}
    </select>
  </section>
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
  <p>
    {correctGuess === true
      ? `Correct! You guessed it in ${guesses} guesses`
      : `Incorrect! ${guesses} guesses.`}
  </p>
  <br />
  <section class="scores">
    <h2>Previous Scores:</h2>
    {#each previousGames as game, index}
      <p>Game: {game} Guesses: {previousGuesses[index]}</p>
      <br />
    {/each}
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
    padding: 50px 10px;
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
</style>
