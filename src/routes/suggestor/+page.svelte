<script>
    let platform = "any"
    let genre = "any"
    let year="2023"

    let changePlatform = () => {
        platform = document.getElementById("platformSelect")?.value;
    }
    let changeGenre = () => {
        genre = document.getElementById("genreSelect")?.value;
    }
    let changeYear = () => {
        year = document.getElementById("year")?.value;
    }
</script>

<section class="options">
    <label for ="platformSelect">Platform:</label>
    <select name="platform" id="platformSelect" 
    on:change={changePlatform}>
        <option value="any">Any</option>
        <option value="PC">PC</option>
        <option value="Switch">Switch</option>
        <option value="Playstation">Playstation</option>
        <option value="Xbox">Xbox</option>
    </select>

    <label for="genreSelect">Genre:</label>
    <select name="genre" id="genreSelect" 
    on:change={changeGenre}>
        <option value="any">Any</option>
        <option value="RPG">RPG</option>
        <option value="FPS">FPS</option>
        <option value="Platformer">Platformer</option>
        <option value="Puzzle">Puzzle</option>
    </select>

    <section class="yearSelector">
        <label for="year">Year:</label>
        <input type="range" id="year" name="year" 
        min="2000" max="2023" value="2023"
        list="yearMarkers"
        on:change={changeYear}>
        <datalist id="yearMarkers">
            <option value="2000" label="2000"></option>
            <option value="2005" label="2005"></option>
            <option value="2010" label="2010"></option>
            <option value="2015" label="2015"></option>
            <option value="2020" label="2020"></option>
        </datalist>
    </section>
</section>

<details class="selected">
    <summary>Current Settings</summary>
    <ul>
        <li>{platform}</li>
        <li>{genre}</li>
        <li>{year}</li>
    </ul>
</details>

<style>
    .options{
        padding: 0px 10px;
    }
    input[type="range"]{
        width: 200px;
    }
    datalist{
        display: flex;
        justify-content: space-between;
        width: 200px;
        padding-left: 350px;
    }
    datalist option{
        color: white;
    }
    label{
        width: 50px;
    }
    select{
        width: 100px;
    }
    .yearSelector{
        display: inline;
    }
    .selected{
        margin: 10px;
        padding: 5px;
    }
    .selected ul{
        padding: 5px;
        color: black;
        background-color: var(--highlightText);
        width: fit-content;
        border-radius: 10px;
    }
</style>