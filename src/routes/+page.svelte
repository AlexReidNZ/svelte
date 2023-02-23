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
    let answer = 21;
    let correct = false;

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
        multiplier = 2;
        correct = false;
    }

    let checkAnswer = () =>
    {
        if (answer === count)
        {
            correct = true;
        }
        else
        {
            correct = false;
        }
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

<p>

</p>

<button on:click={checkAnswer}>
    Check
</button>

<button on:click={reset} style="background-color: rgb(211, 80, 57);">
    reset
</button>

<p>
    {correct === true ? 'Correct!' : 'Incorrect'}
</p>