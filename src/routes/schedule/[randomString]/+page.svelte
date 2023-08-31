<script>
  import Nav from '../../Nav.svelte'
  import { page } from '$app/stores';

  // Parse the query parameters from the URL
  const url = new URL($page.url);
  const queryParams = url.searchParams;

  // Get the "date" parameter as an array
  const dates = queryParams.getAll('date');
</script>

<Nav />
<main class="container">
  <hgroup>
  <h1>Press the dates that you are available.</h1>
<h2>A message will be sent to the person who created this with your answer.</h2>
</hgroup>
  <ul>
    {#each dates as date}
        <button>{date}</button>
    {/each}
  </ul>
</main>

<style>
  /* Your styling here */
</style>
