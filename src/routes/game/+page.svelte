<!-- JS function -->
<script>
    let title = "Number Guess";
    let count = 0;
    let answer = Math.floor(Math.random()*21); //generates a random number from 1-20
    let correct = false;
    let highLow = "";
    let guesses = 0;
    let previousGuesses = 0;
    let previousGame = 0;

    let changeGuess = () =>
    {
        count = document.getElementById("guess").value;
        //sets the value of the players guess to the value in the input.
    }

    let incrementCount = () =>
    {
        count++;
    }

    let decrementCount = () =>
    {
        count--;
    }

    let reset = () => //resets the game by resetting the random number, guesses and count.
    {
        count = 0;
        guesses = 0;
        answer = Math.floor(Math.random()*21);
        highLow = "";
        correct = false;
    }

    let checkAnswer = () => 
    {
        guesses++;
        if (answer == count)//if the guess is correct, correct is true.
        {
            correct = true;
            highLow = "";
            previousGuesses = guesses;
            previousGame = answer;
        }
        else
        {
            correct = false;

            if (answer < count)//shows if the guess is too high or too low.
            {
                highLow = "too high";
            }
            else
            {
                highLow = "too low";
            }
        }
    }
</script>

<!-- HTML Structure --->
<h1>{title}</h1>

<form>
    <input type="number" id="guess" name="guess" min="1" max="20" placeholder="1" on:change={changeGuess}> <!--input for guessing-->
</form>

<section class="buttons">
    <button class="checkButton" on:click={checkAnswer}> <!--checks if the answer is correct-->
        Check
    </button>
    <button class="resetButton" on:click={reset}> <!--lets player reset the game-->
        Reset
    </button>
</section>
<p>
    {correct === true ? `Correct! You guessed it in ${guesses} guesses` : 'Incorrect!'} {highLow}
</p>
<br>
<p>
    Previous Game: <br>
    Number: {previousGame} Guesses: {previousGuesses}
</p>

<!-- styling -->
<style>
h1{
    font-size: 30px;
    font-style: italic;
    font-weight: normal;
    display: flex;
    justify-content: center;
    margin: 0px;
}
p{
    display: flex;
    justify-content: center;
}
form{
    display: flex;
    justify-content: center;
    margin: 10px;
    margin-bottom: 0px;
}
form input{
    background-color: rgba(0, 0, 0, 0);
    height: 25px;
    font-size: 25px;
    color: var(--bodyText);
}
.buttons{
    display: flex;
    justify-content: center;
}
button{
    display: flex;
    justify-content: center;
    margin: 10px;
    width: 80px;
}
.resetButton{
    background-color: rgb(204, 55, 55);
}
.resetButton:hover{
    background-color: rgb(255, 0, 0);
    border-color: rgb(255, 0, 0);
}

.checkButton{
    background-color: rgb(80, 136, 80);
}
.checkButton:hover{
    background-color: rgb(26, 204, 26);
    border-color: rgb(26, 204, 26);
}
</style>