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
  let sorter;
  let ascDesc;
  let games = data;

  const genres = ["Platformer", "Puzzle", "RPG", "Shooter", "Adventure"];
  const platforms = ["PC", "Nintendo", "PS", "Xbox", "iOS"];
  const years = [
    2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011,
    2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020,
  ];
  const sortOptions = ["Title", "Genre", "Developer", "Release Year"];

 
  let sort = () => { //Sorts the data in different ways depending on a user selected sorter
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
        else if (data[i].Genre.includes(genre)) {
          games = [...games, data[i]];
        }
      }
    }
  };
</script>

<section class="container">
  <section class="options">
    <section class="filterSeperator">
      <label for="platformSelect">Platform:</label>
      <select name="platform" id="platformSelect" class="platformSelect" bind:value={platform} on:change={displayData}>
        <option value="">Any</option>
        {#each platforms as platform}
          <option value={platform}>{platform}</option>
        {/each}
      </select>
    </section>
    <section class="filterSeperator">
      <label for="genreSelect">Genre:</label>
      <select name="genre" id="genreSelect" class="genreSelect" bind:value={genre} on:change={displayData}>
        <option value="" selected>Any</option>
        {#each genres as genre}
          <option value={genre}>{genre}</option>
        {/each}
        <option value="Other">Other</option>
      </select>
    </section>
    <section class="filterSeperator">
      <label for="firstYearSelect">Year:</label>
      <select name="firstYear" id="firstYearSelect" class="firstYearSelect" bind:value={firstYear} on:change={displayData}>
        {#each years as year}
          {#if year <= lastYear}
            <option value={year}>{year}</option>
          {/if}
        {/each}
      </select>
      <label for="lastYearSelect">-</label>
      <select name="lastYear" id="lastYearSelect" class="lastYearSelect" bind:value={lastYear} on:change={displayData}>
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
      <select name="sort" id="sortSelect" class="sortSelect" bind:value={sorter} on:change={sort}>
        {#each sortOptions as option}
          <option value={option}>{option}</option>
        {/each}
      </select>
      <select name="ascDesc" id="ascDesc" class="ascDesc" bind:value={ascDesc} on:change={sort}>
        <option value="ascending">Ascending</option>
        <option value="descending">descending</option>
      </select>
    </section>
  </section>

  <section class="centerSettings">
    <details>
      <!--Displays the currently selected filters-->
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
  label, select, details ul, .filterSeperator {
    width: fit-content;
  }
  .options {
    padding-top: 10px;
    display: flex;
    justify-content: space-evenly;
  }
  label {
    padding-right: 5px;
  }
  select {
    height: 25px;
    background-color: var(--darkColour);
    color: var(--bodyText);
    border-color: var(--highlightText);
    border-radius: 10px;
  }
  .centerSettings, details {
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
    list-style-type: none;
  }
  details ul li {
    margin-right: 10px;
    display: inline;
  }
  .filterSeperator {
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
