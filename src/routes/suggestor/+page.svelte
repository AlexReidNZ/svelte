<script>
  let platform = "any";
  let genre = "any";
  let year = "2023";

  let changePlatform = () => {
    platform = document.getElementById("platformSelect")?.value;
  };
  let changeGenre = () => {
    genre = document.getElementById("genreSelect")?.value;
  };
  let changeYear = () => {
    year = document.getElementById("year")?.value;
  };
</script>

<section class="options"> <!--Section that contains inputs for options-->
  <label for="platformSelect">Platform:</label>
  <select name="platform" id="platformSelect" on:change={changePlatform}>
    <option value="any">Any</option>
    <option value="PC">PC</option>
    <option value="Switch">Switch</option>
    <option value="Playstation">Playstation</option>
    <option value="Xbox">Xbox</option>
  </select>

  <label for="genreSelect">Genre:</label>
  <select name="genre" id="genreSelect" on:change={changeGenre}>
    <option value="any">Any</option>
    <option value="RPG">RPG</option>
    <option value="FPS">FPS</option>
    <option value="Platformer">Platformer</option>
    <option value="Puzzle">Puzzle</option>
  </select>

  <section class="yearSelector"> <!--Contains slider for selecting year-->
    <label for="year">Year:</label>
    <input
      type="range"
      id="year"
      name="year"
      min="2000"
      max="2023"
      value="2023"
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

<details class="selected"> <!--Displays the currently selected options-->
  <summary>Current Settings</summary>
  <ul>
    <li>Platform: {platform}</li>
    <li>Genre: {genre}</li>
    <li>Year: {year}</li>
  </ul>
</details>

<style>
  .options {
    padding: 0px 10px;
    display: flex;
    justify-content: center;
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
    justify-content: space-between;
    width: 200px;
    padding-left: 40px;
  }
  datalist option {
    color: white;
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
    margin-right: 10px;
  }
  .yearSelector {
    display: inline;
  }
  .selected {
    margin: 10px;
    padding: 5px;
  }
  .selected ul {
    margin: 0;
    padding: 5px;
    color: black;
    background-color: var(--highlightText);
    width: fit-content;
    border-radius: 10px;
    list-style-type: none;
  }
</style>
