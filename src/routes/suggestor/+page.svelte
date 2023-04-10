<script>
  import { data } from "../../../gamedata.js";

  let platform = "";
  let genre = "";
  let year = 2020;
  let game = data;

  let genres = ["Platformer", "Puzzle", "RPG", "Shooter", "Adventure"];
  let platforms = ["PC", "Nintendo", "PS", "Xbox","iOS"];

  console.log(data);

  let changePlatform = () => {
    let temp = document.getElementById("platformSelect")?.value;
    platform = temp;
  };
  let changeGenre = () => {
    let temp = document.getElementById("genreSelect")?.value;
    genre = temp;
  };
  let changeYear = () => {
    let temp = document.getElementById("year")?.value;
    year = temp;
  };
  let displayData = () => {
    game = [];
    let count = 0;

    for (let i = 0; i < data.length; i++) {
      if (data[i].ReleaseYear <= year && data[i].Platforms.includes(platform)) {
        //if Platform and year match
        if (genre == "Other") {
          //If other is selected, check that each game DOESN'T have any of the listed genres
          let isOther = true;
          for (let x = 0; x < genres.length; x++) {
            if (data[i].Genre.includes(genres[x])) {
              isOther = false;
            }
          }
          if (isOther) {
            //Add all 'other' games
            game[count] = data[i];
            count++;
          }
        }
        if (data[i].Genre.includes(genre)) {
          //If a genre is selected, add all games of that genre
          game[count] = data[i];
          count++;
        }
      }
    }
  };
</script>

<section class="options">
  <!--Section that contains inputs for options-->
  <section class="filterSeperator">
    <label for="platformSelect">Platform:</label>
    <select name="platform" id="platformSelect" on:change={changePlatform}>
      <option value="">Any</option>
      {#each platforms as platform}
        <option value={platform}>{platform}</option>
      {/each}
    </select>
  </section>
  <section class="filterSeperator">
    <label for="genreSelect">Genre:</label>
    <select name="genre" id="genreSelect" on:change={changeGenre}>
      <option value="">Any</option>
      {#each genres as genre}
        <option value={genre}>{genre}</option>
      {/each}
      <option value="Other">Other</option>
    </select>
  </section>
  <section class="filterSeperator">
    <!--Contains slider for selecting year-->
    <label for="year">Year:</label>
    <input
      type="range"
      id="year"
      name="year"
      min="2000"
      max="2020"
      value="2020"
      list="yearMarkers"
      on:change={changeYear}
    />
    <datalist id="yearMarkers">
      <option value="2000" label="2000" />
      <option value="2005" label="2005" />
      <option value="2010" label="2010" />
      <option value="2015" label="2015" />
      <option value="2020" label="2020" />
    </datalist>
  </section>
</section>

<details>
  <!--Displays the currently selected options-->
  <summary>Current Settings</summary>
  <ul>
    <li>Platform: {platform}</li>
    <li>Genre: {genre}</li>
    <li>Year: {year}</li>
  </ul>
</details>

<button on:click={displayData}>Display</button><br />

<section class = "DisplayedList">
  <span><h1>Title</h1><h1>Genre</h1><h1>Platforms</h1><h1>Release Year</h1></span>
{#each game as g}
  <span><p>{g.Title}</p><p>{g.Genre}</p><p>{g.Platforms}</p><p>{g.ReleaseYear}</p></span>
{/each}
</section>

<style>
  .options {
    padding-top: 10px;
    display: flex;
    justify-content: space-evenly;
  }
  input[type="range"] {
    width: 200px;
    color: var(--highlightText);
  }
  input[type="range"]::-webkit-slider-runnable-track {
    background-color: var(--darkColour);
    cursor: default;
    border-radius: 10px;
  }
  datalist {
    display: flex;
    justify-content: space-evenly;
    width: 200px;
    padding-left: 40px;
  }
  datalist option {
    color: white;
    padding: 0px 7px;
  }
  label {
    width: fit-content;
    padding-right: 5px;
  }
  select {
    width: fit-content;
    height: 25px;
    background-color: var(--darkColour);
    color: var(--bodyText);
    border-color: var(--highlightText);
    border-radius: 10px;
  }
  details {
    display: flex;
    justify-content: center;
    margin: 10px;
  }
  details ul {
    margin: 0px;
    padding: 5px;
    background-color: var(--darkColour);
    color: var(--bodyText);
    border-radius: 10px;
    border: 1px;
    border-color: var(--highlightText);
    border-style: solid;
    width: fit-content;
    list-style-type: none;
  }
  details ul li {
    margin-right: 10px;
    display: inline;
  }
  .filterSeperator {
    width: fit-content;
    height: fit-content;
  }
  button {
    background-color: var(--highlightText);
    margin-right: 5px;
    margin-bottom: 5px;
    margin-top: 5px;
  }
  button:hover {
    background-color: var(--secondaryHighlight);
    color: var(--bodyText);
  }
  span{
    display: flex;
    padding: 5px 0;
  }
  span p{
    width: 25%;
    text-align: center;
  }
  span h1{
    color: var(--highlightText);
    width: 25%;
    text-align: center;
  }
</style>
