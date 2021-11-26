<!-- Individual Pokemon Page-->

<!-- Query before page load-->
<script context="module">
  export async function load({page}) {
    const id = page.params.id;
    const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
    const res = await fetch(url);
    const pokeman = await res.json();
    return {props: {pokeman}};
  }
</script>

<!-- Page should now have the queried pokemon so display them-->
<script>
  export let pokeman;
  const type = pokeman.types[0].type.name; //get specific nested value from the pokemon
</script>

<!--Display the pokemon name, height, type, weight, image to the user-->
<div class="flex flex-col items-center">
  <h1 class=" text-4xl text-center my-8 uppercase">{pokeman.name}</h1>
  <p>Type: <strong>{type}</strong> | Height: {pokeman.height} | Weight: {pokeman.weight}</p>
  <img class="card-image" src={pokeman.sprites['front_default']} alt={pokeman.name}>
</div>