<script>
    // const BASE_URL = "https://www.giantbomb.com/api";

    // fetch(
    //     `${BASE_URL}/games/?api_key=cb638b4d991587308456a3533f0914df1b87309d&format=json&field_list=name`
    // )
    //     .then((res) => res.json)
    //     .then((data) => {
    //         console.log(data);
    //     });
</script>

<section>
    <h1>Welcome to Gamedle!</h1>
    <br>
    <p>
        See the <a href="about">about page</a> to learn more, or if you already
        know what you're doing here, go straight to the
        <a href="suggestor">game suggestor</a>
        or <a href="game">play a game!</a>
    </p>
</section>

<style>

    section {
        padding-top: 5vh;
        display: flex;
        flex-direction: column;
    }
    p{
        align-self: center;
    }
    a {
        color: var(--highlightText);
        text-decoration: underline;
        text-decoration-color: var(--highlightText);
    }
    a:visited {
        color: var(--highlightText);
        text-decoration: underline;
        text-decoration-color: var(--highlightText);
    }
    a:hover {
        color: var(--mainText);
    }
    h1 {
        color: var(--highlightText);
        align-self: center;
        margin: 0;
    }
</style>
