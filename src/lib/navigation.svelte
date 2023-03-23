<script>
    import {page} from '$app/stores';
</script>

<nav>
    <ul>
        <li><button class:active="{$page.url.pathname==="/"}"><a href="/">Home</a></button></li>
        <li><button class:active="{$page.url.pathname.includes("about")}"><a href="about" >about</a></button></li>
        <li><button class:active="{$page.url.pathname.includes("suggestor")}"><a href = "suggestor">Suggestor</a></button></li>
        <li><button class:active="{$page.url.pathname.includes("game")}"><a href = "game">Play</a></button></li>
    </ul>
</nav>

<!-- styling -->
<style>
nav{
    height: 5vh;
    min-height: 25px;
    width: 100%;
    background-color: var(--darkColour);
}
button{
    background-color: var(--highlightText);
    margin-right: 5px;
    margin-bottom: 5px;
    margin-top: 5px;
}
button:hover{
    background-color: var(--secondaryHighlight);
}
a{
    display: block;
    padding: 8px;
    color: black;
    text-decoration: underline var(--secondaryHighlight);
}
a:hover{
    color: white;
    text-decoration: underline var(--highlightText);
}
ul{
    list-style-type: none;
    display: flex;
    justify-content: center;
    margin: 0px;
}
li{
    display: inline;
}
.active{
    background-color: var(--secondaryHighlight);
}
.active a{
    color: white;
    text-decoration: underline var(--highlightText);
}
</style>