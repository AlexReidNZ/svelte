<!-- CSS style -->
<style>
    h1{
        color: rgb(23, 56, 245);
        font-size: 24px;
        font-style: italic;
        font-weight: normal;
    }

    button{
        border-radius: 100px;
    }
</style>

<!-- JS function -->
<script>
    let title = "Number Guess";
    let count = 0;
    let multiplier = 2;
    let answer = Math.floor(Math.random() * 21);
    let correct = false;
    let highLow = "";
    let guesses = 0;
    let previousGame = 0;
    let previousGuesses = 0;

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
        multiplier = 2;
        correct = false;
        answer = Math.floor(Math.random() * 21);
        highLow = "";
    }

    let checkAnswer = () =>
    {
        guesses++;
        if (answer === count)
        {
            correct = true;
            highLow = "";
            previousGame = count;
            previousGuesses = guesses;
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

    let previousGames = () =>
    {

    }
</script>

<!-- HTML Structure --->
<h1>{title}</h1>

<p>
    {count}
</p>

<button on:click={incrementCount}>
    increase
</button>

<button on:click={decrementCount}>
    decrease
</button>

<br>

<button on:click={checkAnswer}>
    Check
</button>

<button on:click={reset} style="background-color: rgb(211, 80, 57);">
    reset
</button>

<p>
    {correct === true ? `Correct! ${guesses} guesses` : 'Incorrect'} {highLow}
</p>

<p>
    Record: <br>
    Previous game: <br>
    Number:{previousGame} guesses:{previousGuesses}
</p>