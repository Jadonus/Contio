<script>
  import Nav from '../../Nav.svelte'
  import { page } from '$app/stores';
    import { onMount } from 'svelte';
  let show = false; // Declare show at a higher scope level

  // Parse the query parameters from the URL
  const url = new URL($page.url);
  const queryParams = url.searchParams;

  // Get the "date" parameter as an array
 function formatDateTime(dateTimeString) {
    const options = { year: 'numeric', month: 'long', day: 'numeric', hour: 'numeric', minute: 'numeric' };
    const dateTime = new Date(dateTimeString);
    return dateTime.toLocaleString('en-US', options);
  }
const dates = queryParams.getAll('date');
  const hi = dates.map(date => formatDateTime(date));
let modal= false
  function showAlertIfNoDates() {
    if (hi.length === 0) {
      modal = true
    }
  }
 onMount(() => {
    showAlertIfNoDates();
  });
  let name = ''; // Store the user's name
  let selectedDate = ''; // Store the selected date
  let xOriginUrl = ''// Set the default value to the current page's URL
  onMount(() => xOriginUrl = window.location.href);

   async function handleSubmit() {
    try {
      const response = await fetch('http://contio-backend.vercel.app/meeting/submit/', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ name, date: selectedDate, x_origin_url: xOriginUrl }) // Include x-origin-url in the body
      });
      if (response.ok) {
        console.log('Response sent successfully!');
        show = true
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
    <h2>A message will be sent to the person who created this with your answer. Please only pick one date.</h2>
  </hgroup>
  
  <ul>
  <input placeholder="Name" type="text" bind:value={name}>
<div class="grid">
  {#each hi as date}
    <div>
      <button class={selectedDate === date ? '' : 'secondary'} on:click={() => selectedDate = date}>{date}</button>
    </div>
  {/each}
</div>
{#if name}
<button class={show ? 'success' : ''} on:click={handleSubmit}>
  {show ? '✔ Success' : 'Submit'}
</button>
{/if}
  </ul>
{#if modal}
<dialog open>
  <header><h1>Sorry, This link is not valid, Please try another link.</h1></header>
</dialog>


{/if}
</main>

<style lang="scss">
.success {
  background-color: #e8f5e9;
  color: darkgreen;
  border-width: 0px
}
/* Your styling here */
</style>
