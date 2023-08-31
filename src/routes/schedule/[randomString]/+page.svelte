<script>
  import Nav from '../../Nav.svelte'
  import { page } from '$app/stores';

  // Parse the query parameters from the URL
  const url = new URL($page.url);
  const queryParams = url.searchParams;

  // Get the "date" parameter as an array
  const dates = queryParams.getAll('date');

  let name = ''; // Store the user's name
  let selectedDate = ''; // Store the selected date

  async function handleSubmit() {
    try {
      // Send the name and selectedDate to the backend using fetch
      const response = await fetch('http://127.0.0.1:8000/api/submit/', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ name, date: selectedDate })
      });

      if (response.ok) {
        console.log('Response sent successfully!');
      } else {
        console.error('Failed to send response.');
      }
    } catch (error) {
      console.error('An error occurred:', error);
    }
  }
</script>

<Nav />
<main class="container">
  <hgroup>
    <h1>Enter your name and press on the dates that you are available.</h1>
    <h2>A message will be sent to the person who created this with your answer. Pl</h2>
  </hgroup>
  
  <ul>
  <input placeholder="Name" type="text" bind:value={name}> <!-- Capture the user's name -->

<div class="grid">
  {#each dates as date}
    <div>
      <button  on:click={() => selectedDate = date}>{date}</button>
    </div>
  {/each}
</div>
{#if name }
  <button on:click={handleSubmit}>Submit</button> <!-- Call handleSubmit when submit button clicked -->
{/if}
  </ul>

</main>

<style>
 
/* Your styling here */
</style>