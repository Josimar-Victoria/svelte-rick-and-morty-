<script>
  import Character from "./libs/Character.svelte";
  let characters = [];
  let page = 1;

  async function loadCharacters() {
    const response = await fetch(
      `https://rickandmortyapi.com/api/character?page=${page}`
    );
    const data = await response.json();
    characters = data.results;
    console.log({ characters });
  }

  loadCharacters();

  function handlePreviousPage() {
    page--;
    loadCharacters();
  }

  function handleNextPage() {
    page++;
    loadCharacters();
  }
</script>

<h1 class="titel">Rick and Morty Svelte</h1>

<div class="container">
  <div class="btns">
    <button class="btn" on:click={handlePreviousPage} disabled={page === 1}
      >Previous</button
    >
    <button class="btn" on:click={handleNextPage}>Next</button>
  </div>
  <div class="grid">
    {#each characters as character (character.id)}
      <Character {character} />
    {/each}
  </div>
</div>

<style></style>
