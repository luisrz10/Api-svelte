<script>
  import Character from "./lib/Character.svelte";
  
    let characters = [];
    let page = 1;
  
    async function loadCharacters() {
      const response = await   fetch("https://rickandmortyapi.com/api/character?page=" + page);
      const data = await response.json()
      characters = data.results;
    }
    loadCharacters();
  
    function nextpage() {
      page++;
      loadCharacters()
    }
  
    function previouspage() {
      page--;
      loadCharacters()
    }
  </script>
  
  <h1 class="title">Rick and Morty</h1>
  
  
  <div class="container">
    <div class="btns">
      <button class="btn" on:click={previouspage} disabled={page === 1}> atras</button>
      <button class="btn" on:click={nextpage}>siguiente</button>
    </div>
    <div class="grid">
    {#each characters as character}
    <Character {character} />
    {/each}
    </div>
  </div>