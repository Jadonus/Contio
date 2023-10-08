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

const time = queryParams.getAll('time');
  const hi = dates.map(date => formatDateTime(date));
let modal= false
  function showAlertIfNoDates() {
    if (hi.length === 0) {
      modal = true
    }
  }
let edittime = JSON.stringify(time)
console.log("time" + edittime)
 onMount(() => {
    showAlertIfNoDates();
  });
  let name = ''; // Store the user's name
  let selectedDate = ''; // Store the selected date
  let xOriginUrl = ''// Set the default value to the current page's URL
  onMount(() => xOriginUrl = window.location.href);

   async function handleSubmit() {
    try {
      const response = await fetch('https://contio-backend.vercel.app/meeting/submit/', {
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
const timeArray = JSON.parse(edittime);
function formatTimeLeft(milliseconds) {
  const seconds = Math.floor(milliseconds / 1000);
  const days = Math.floor(seconds / 86400); // Number of seconds in a day
  const hours = Math.floor((seconds % 86400) / 3600); // Number of seconds in an hour
  const minutes = Math.floor(((seconds % 86400) % 3600) / 60); // Number of seconds in a minute
  
  return `${days} day(s), ${hours} hour(s), and ${minutes} minute(s)`
}
// Access the first item in the 'timeArray' to get the date-time string
const exampleTime = new Date(timeArray[0]);

exampleTime.setDate(exampleTime.getDate());
console.log(exampleTime)
// Calculate the time difference in milliseconds
const timeDifference = exampleTime - new Date() ; 
console.log(timeDifference)
// Initialize timeLeft with the time difference
let timeLeft = timeDifference > 0 ? timeDifference : 0;
let countdown
// Create a Svelte reactive variable for time display
let timeLeftDisplay
function startCountdown() {
  countdown = setInterval(() => {
    timeLeft -= 1000; // Subtract 1 second
    if (timeLeft <= 0) {
      clearInterval(countdown);
      modal = true; // Time's up, show the modal!

    console.log(exampleTime)
    } else {
      timeLeftDisplay = formatTimeLeft(timeLeft); // Update the time left display reactively
    console.log(timeLeftDisplay)
      }

  }, 1000); // Update every second
}
  startCountdown()
// Update the timeLeft and start the countdown
</script>

<Nav />

<main class="container">
  <hgroup>
    <h1>Enter your name and press on the dates that you are available.</h1>
    <h2>A message will be sent to the person who created this with your answer. Please only pick one date. You have {timeLeftDisplay} left to answer before your response is discarded.</h2>
  </hgroup>
  
  <input placeholder="Name" type="text" bind:value={name}>
<div class="grid">
  {#each hi as date}
      <button class={selectedDate === date ? '' : 'secondary'} on:click={() => selectedDate = date}>{date}</button>
  {/each}

</div>
{#if name}
<div class="grid tpm">
<button class={show ? 'success' : ''} on:click={handleSubmit}>
  {show ? '✔ Success' : 'Submit'}
</button>
</div>
{/if}

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
.tpm {
 margin-top: 1rem; 
}
main {
  font-family: 'Inter', sans-serif;
}
/* Your styling here */
</style>
