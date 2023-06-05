<script>
  /*
    This page dynamically sorts, filters and displays the games from the dataset based on filters selected by the user
  */

  import { data } from "../../../gamedata.js";
  data.sort((a, b) => {
    return a.Title.localeCompare(b.Title);
  });

  let platform = "";
  let genre = "";
  let firstYear = 2000;
  let lastYear = 2020;
  let sorter = "Title";
  let games = data;

  const genres = ["Platformer", "Puzzle", "RPG", "Shooter", "Adventure"];
  const platforms = ["PC", "Nintendo", "PS", "Xbox", "iOS"];
  const years = [
    2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011,
    2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020,
  ];
  const sortOptions = ["Title", "Genre", "Developer", "Release Year"];

  let changePlatform = () => {
    platform = document.querySelector("select.platformSelect")?.value;
    displayData();
  };
  let changeGenre = () => {
    genre = document.querySelector("select.genreSelect")?.value;
    displayData();
  };
  let changeFirstYear = () => {
    firstYear = document.querySelector("select.firstYearSelect")?.value;
    displayData();
  };
  let changeLastYear = () => {
    lastYear = document.querySelector("select.lastYearSelect")?.value;
    displayData();
  };
  //Sorts the data in diffeent ways depending on a user selected sorter
  let sort = () => {
    sorter = document.querySelector("select.sortSelect")?.value;
    let ascDesc = document.querySelector("select.ascDesc")?.value;

    if (sorter == "Title") {
      data.sort((a, b) => {
        return a.Title.localeCompare(b.Title);
      });
    }
    if (sorter == "Genre") {
      data.sort((a, b) => {
        return a.Genre.localeCompare(b.Genre);
      });
    }
    if (sorter == "Developer") {
      data.sort((a, b) => {
        return a.Developer.localeCompare(b.Developer);
      });
    }
    if (sorter == "Release Year") {
      data.sort((a, b) => {
        return a.ReleaseYear - b.ReleaseYear;
      });
    }

    if (ascDesc == "descending") {
      data.reverse();
    }

    games = data;
    displayData();
  };
  let displayData = () => {
    games = [];

    for (let i = 0; i < data.length; i++) {
      if (
        data[i].ReleaseYear <= lastYear &&
        data[i].ReleaseYear >= firstYear &&
        data[i].Platforms.includes(platform)
      ) {
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
            games = [...games, data[i]];
          }
        }
        if (data[i].Genre.includes(genre)) {
          games = [...games, data[i]];
        }
      }
    }
  };
</script>

<section class="container">
  <section class="options">
    <!--Section that contains inputs for options-->
    <section class="filterSeperator">
      <label for="platformSelect">Platform:</label>
      <select
        name="platform"
        id="platformSelect"
        class="platformSelect"
        on:change={changePlatform}
      >
        <option value="">Any</option>
        {#each platforms as platform}
          <option value={platform}>{platform}</option>
        {/each}
      </select>
    </section>
    <section class="filterSeperator">
      <label for="genreSelect">Genre:</label>
      <select
        name="genre"
        id="genreSelect"
        class="genreSelect"
        on:change={changeGenre}
      >
        <option value="">Any</option>
        {#each genres as genre}
          <option value={genre}>{genre}</option>
        {/each}
        <option value="Other">Other</option>
      </select>
    </section>
    <section class="filterSeperator">
      <label for="firstYearSelect">Year:</label>
      <select
        name="firstYear"
        id="firstYearSelect"
        class="firstYearSelect"
        on:change={changeFirstYear}
      >
        {#each years as year}
          {#if year <= lastYear}
            <option value={year}>{year}</option>
          {/if}
        {/each}
      </select>
      <label for="lastYearSelect">-</label>
      <select
        name="lastYear"
        id="lastYearSelect"
        class="lastYearSelect"
        on:change={changeLastYear}
      >
        {#each years as year}
          {#if year >= firstYear}
            <option value={year}>{year}</option>
          {/if}
        {/each}
        <option value="" selected hidden disabled>2020</option>
        <!--Will be shown by default at the start-->
      </select>
    </section>
    <section class="filterSeperator">
      <label for="sortSelect">Sort by:</label>
      <select name="sort" id="sortSelect" class="sortSelect" on:change={sort}>
        {#each sortOptions as option}
          <option value={option}>{option}</option>
        {/each}
      </select>
      <select name="ascDesc" id="ascDesc" class="ascDesc" on:change={sort}>
        <option value="ascending">Ascending</option>
        <option value="descending">descending</option>
      </select>
    </section>
  </section>

  <section class="centerSettings">
    <details>
      <!--Displays the currently selected options-->
      <summary>Current Settings</summary>
      <ul>
        {#if platform == ""}
          <li>Platform: Any</li>
        {:else}
          <li>Platform: {platform}</li>
        {/if}
        {#if genre == ""}
          <li>Genre: Any</li>
        {:else}
          <li>Genre: {genre}</li>
        {/if}
        <li>Year: {firstYear}-{lastYear}</li>
        <li>Sorted By: {sorter}</li>
      </ul>
    </details>
  </section>

  <section class="DisplayedList">
    <h2>You Should Play...</h2>
    <span>
      <h2>Title</h2>
      <h2>Genre</h2>
      <h2>Platforms</h2>
      <h2>Developer</h2>
      <h2>Release Year</h2>
    </span>
    {#each games as g}
      <span
        ><p>{g.Title}</p>
        <p>{g.Genre}</p>
        <p>{g.Platforms}</p>
        <p>{g.Developer}</p>
        <p>{g.ReleaseYear}</p></span
      >
    {/each}
  </section>
</section>

<style>
  .options {
    padding-top: 10px;
    display: flex;
    justify-content: space-evenly;
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
  .centerSettings,
  details {
    display: flex;
    justify-content: center;
  }
  details {
    margin: 10px;
  }
  details summary {
    align-self: center;
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
  span {
    display: flex;
    padding: 5px 0;
    min-height: 50px;
    min-width: 850px;
  }
  span p {
    width: 20%;
    text-align: center;
  }
  h2 {
    color: var(--highlightText);
    text-align: center;
    margin: 5px;
  }
  span h2 {
    width: 20%;
    font-size: 20px;
  }
</style>
