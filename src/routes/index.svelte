<svelte:head>
  <title>Pokedex Tutorial</title>
</svelte:head>

<!-- Query before page load (Query all 150 1st gen pokemon)-->
<script context="module">
  export async function load({page}) {
    const url = 'https://pokeapi.co/api/v2/pokemon?limit=150';
    const res = await fetch(url);
    const data = await res.json();
    const loadedPokemon = data.results.map((data, index) => {
      return {
        name: data.name,
        id: index + 1,
        image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${index + 1}.png`,
      };
    });
    return {props: {pokemon:loadedPokemon}};
  }
</script>

<!-- Import the pokemon card component and handle searching through the svelete reative $: {} function-->
<script>
    import PokemanCard from '../Components/pokemanCard.svelte';
    export let pokemon;

    let searchTerm = "";
    let filteredPokemon = [];

    $: {
      if (searchTerm) {
        //search for the pokemon. If any piece of the pokeman's name contains the search term, update with only those results
        filteredPokemon = pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()));
      } else {
        filteredPokemon = [... pokemon];
      }
    }

</script>

<h1 class="text-4xl text-center my-8 uppercase">SvelteKit Pokedex Tutorial</h1>

<input class="w-full rounded-md text-lg p-4 border-2 border-gray-200" 
  type="text" bind:value={searchTerm} placeholder="Search Pokemon">

<!-- display each pokemon card to the user. For each filteredPokemon get the individual pokeman and pass it to the pokemanCard component-->
<div class="py-4 grid gap-4 md:grid-cols-2 gr-cols-1">
  {#each filteredPokemon as pokeman}
    <PokemanCard pokeman = {pokeman} />
  {/each}
</div>


