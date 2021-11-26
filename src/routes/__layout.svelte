<!--Layout which handles the imports for tailwind styles, nav import
  and displaying the Nav component along with the svelete "slot" 
  for every web route
-->

<style>
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>

<script>
  import Nav from '../Components/nav.svelte';
</script>

<div class="p-8 max-w-6xl mx-auto">
  <Nav />
  <slot></slot>
</div>
