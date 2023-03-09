<!-- JS function -->
<script>
    let title = "Number Guess";
    let count = 0;
    let answer = Math.floor(Math.random() * 21);
    let correct = false;
    let highLow = "";
    let guesses = 0;
    let previousGuesses = 0;
    let previousGame = 0;

    let incrementCount = () =>
    {
        count++;
    }

    let decrementCount = () =>
    {
        count--;
    }

    let reset = () =>
    {
        count = 0;
        guesses = 0;
        answer = Math.floor(Math.random() * 21);
        highLow = "";
        correct = false;
    }

    let checkAnswer = () =>
    {
        guesses++;
        if (answer === count)
        {
            correct = true;
            highLow = "";
            previousGuesses = guesses;
            previousGame = answer;
        }
        else
        {
            correct = false;

            if (answer < count)
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
<section class = "gameSection">
<h1>{title}</h1>

<p>
    {count}
</p>

<button class="gameButton" on:click={incrementCount}>
    increase
</button>

<button class="gameButton" on:click={decrementCount}>
    decrease
</button>

<br><br>

<button class="checkButton" on:click={checkAnswer}>
    Check
</button>

<button class="resetButton" on:click={reset}>
    reset
</button>

<p>
    {correct === true ? `Correct! ${guesses} guesses` : 'Incorrect!'} {highLow}
</p>

<p>
    Previous Game: <br>
    Number: {previousGame} Guesses: {previousGuesses}
</p>
</section>