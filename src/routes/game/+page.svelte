<script>
  let title = "Guessing Game";
  let guess = 0;
  let secondGuess = 1;
  let thirdGuess = "";
  let answer = Math.floor(Math.random() * 21); //generates a random number from 1-20
  let answer2 = Math.floor(Math.random() * 21);
  let answer3 = "test";
  let correct = false;
  let highLow1 = "";
  let highLow2 = "";
  let correct3 = "";
  let guesses = 0;
  let previousGuesses = 0;
  let previousGame = 0;
  let changeGuess = () => {
    guess = document.getElementById("guess")?.value;
    secondGuess = document.getElementById("secondGuess")?.value;
    thirdGuess = document.getElementById("thirdGuess")?.value;
    //sets the value of the players guesses to the value in the input.
  };
  let reset = () =>
    //resets the game by resetting the random answers, guesses and count.
    {
      guess = 0;
      guesses = 0;
      answer = Math.floor(Math.random() * 21);
      highLow1 = "";
      highLow2 = "";
      correct = false;
    };
  let checkAnswer = () => {
    guesses++;
    if (answer == guess && answer2 == secondGuess && answer3 == thirdGuess) {
      //if the guess is correct, correct is true.
      correct = true;
      highLow1 = "";
      highLow2 = "";
      previousGuesses = guesses;
      previousGame = answer;
    } else {
      correct = false;
      if (answer < guess) {
        //shows if the guess is too high or too low.
        highLow1 = "too high";
      } else if (answer > guess) {
        highLow1 = "too low";
      } else {
        highLow1 = "Correct!";
      }
      if (answer2 < secondGuess) {
        //shows if the guess is too high or too low.
        highLow2 = "too high";
      } else if (answer2 > secondGuess) {
        highLow2 = "too low";
      } else {
        highLow2 = "Correct!";
      }
      if (answer3 == thirdGuess) {
        correct3 = "Correct!";
      } else {
        correct3 = "Incorrect!";
      }
    }
  };
</script>

<h1>{title}</h1>
<form>
  <!--inputs for guessing-->
  <input
    type="number"
    id="guess"
    name="guess"
    min="1"
    max="20"
    placeholder="1"
    on:change={changeGuess}
  />
  <input
    type="number"
    id="secondGuess"
    name="secondGuess"
    min="1"
    max="20"
    placeholder="1"
    on:change={changeGuess}
  />
  <input
    type="text"
    id="thirdGuess"
    name="thirdGuess"
    on:change={changeGuess}
  />
</form>
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
  {highLow1}
  {highLow2}
  {correct3}
</p>
<br />
<p>
  {correct === true ? `Correct! You guessed it in ${guesses} guesses` : ""}
</p>
<br />
<p>
  Previous Game:<br />
  Number: {previousGame} Guesses: {previousGuesses}
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
  form {
    display: flex;
    justify-content: center;
    margin: 10px;
    margin-bottom: 0px;
  }
  form input {
    background-color: rgba(0, 0, 0, 0);
    height: 25px;
    font-size: 25px;
    color: var(--bodyText);
    width: 10rem;
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
