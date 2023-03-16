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
<h1>{title}</h1>

<p>
    {count}
</p>

<section class="buttons">
    <button class="mathButton" on:click={decrementCount}>
        decrease
    </button>
    
    <button class="mathButton" on:click={incrementCount}>
        increase
    </button>


    <button class="checkButton" on:click={checkAnswer}>
        Check
    </button>

    <button class="resetButton" on:click={reset}>
        reset
    </button>
</section>
<p>
    {correct === true ? `Correct! ${guesses} guesses` : 'Incorrect!'} {highLow}
</p>

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
.mathButton{
    background-color: rgb(151, 192, 240);
}
.mathButton:hover{
    background-color: rgb(26, 218, 243);
    border-color: rgb(26, 218, 243);
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