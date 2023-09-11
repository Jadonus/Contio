<script>

  import Nav from "../Nav.svelte";
  import { onMount } from "svelte";

  // Array to store the submitted dates
  let submittedDates = [];
  let generatedLink = "";
let submootedDates = [];
  // Function to handle date submission
  function submitDate(event) {
    const selectedDateTime = event.target.value;

    // Check if the input is not empty and not the default empty value
    if (selectedDateTime && selectedDateTime !== "1970-01-01T00:00") {
      submittedDates = [...submittedDates, selectedDateTime];

      // Format the newly submitted date and add it to the formattedDates array
      const formattedDate = formatDateTime(selectedDateTime);
      formattedDates = [...formattedDates, formattedDate];

      event.target.value = ""; // Clear the input after adding
    }
  }

 function formatDateTime(dateTimeString) {
    const options = { year: 'numeric', month: 'long', day: 'numeric', hour: 'numeric', minute: 'numeric' };
    const dateTime = new Date(dateTimeString);
    return dateTime.toLocaleString('en-US', options);
  }
  let formattedDates = submittedDates.map(date => formatDateTime(date));




let dateInput;
onMount(() => {
  dateInput = document.querySelector('input[type="datetime-local"]');
  dateInput.min = new Date().toISOString().slice(0, 16);
  dateInput.addEventListener("blur", submitDate);



});




  // Function to generate a random string
  const randomWords =["advertise", "arise", "afford", "assumption", "album", "ample", "agile", "attract", "approach", "aquarium", "adviser", "aviation", "automatic", "appear", "applied", "abuse", "adult", "amuse", "architect", "archive", "artist", "articulate", "arrange", "arm", "addition", "arrangement", "astonishing", "absolute", "arrogant", "at", "apparatus", "activate", "aware", "accident", "admission", "asset", "appendix", "appointment", "abundant", "avenue", "annual", "apathy", "adopt", "analysis", "amputate", "attitude", "advantage", "aluminium", "acceptance", "accompany"]

  // Function to generate random string from random words
 function generateRandomString(length) {
    let result = "";
    for (let i = 0; i < length; i++) {
      const randomIndex = Math.floor(Math.random() * randomWords.length);
      result += randomWords[randomIndex];
    }
    return result;
  }

  // Function to generate the link
  let generatedLinkText = "";

async function makePostRequest(data) {
  try {
    const response = await fetch('https://contio-backend.vercel.app/meeting/submit/new', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(data),
    });

    if (response.ok) {
      console.log('POST request successful!');
    } else {
      console.error('POST request failed!');
    }
  } catch (error) {
    console.error('Error while making POST request:', error);
  }
}
let email = '' 
// Inside your generateLink function, after generating the link:
function generateLink() {
  const randomString = generateRandomString(3);
  const dateParams = submittedDates.map((date) => `date=${date}`).join("&");
  const link = `http://contio.vercel.app/schedule/${randomString}?${dateParams}`;
  generatedLink = link; // Store the link for display
  generatedLinkText = generatedLink;

  // Now, let's create the data to send to your backend
  const postData = {
    timeOfRequest: new Date().toISOString(), // Get the current time as ISO string
    generatedLink: generatedLink,
    email: email
  };

  // Make the POST request
  makePostRequest(postData);
}

  // Function to close the modal
  function closeModal() {
    const modal = document.querySelector("dialog[open]");
    if (modal) {
      modal.removeAttribute("open");
    }
  }

  let pop = false;

  const copyContent = async () => {
    try {
      await navigator.clipboard.writeText(generatedLinkText);
      console.log('Content copied to clipboard');
      pop = true;
    } catch (err) {
      console.error('Failed to copy: ', err);
    }
  }
</script>

<Nav />
<header class="container">
  <hgroup>
    <h1>When are you available?</h1>
    <h2>Pick a couple times when you are available to meet.</h2>
  </hgroup>
  <div class="grid">
  <div><input type="datetime-local" min="{new Date().toISOString().slice(0, 16) }" /></div>

  <div><input type="email" bind:value={email} placeholder="Your Email." /></div>
</div>
</header>

<div class="container">
  <ul>
    {#each formattedDates as date}
      <li>{date}</li>
    {/each}
  </ul>

<button role="button" on:click={generateLink} disabled={!submittedDates.length}>Generate link from dates</button>


  {#if generatedLink}
    <dialog open>
      <article>
        <header>
          <a
            href="#cancel"
            data-target="modal-example"
            on:click|preventDefault={closeModal}
            aria-label="Close"
            class="close"
          />
          <h2>Beep boop beep! 🤖 Your link is ready!</h2>
        </header>
        {#if pop}
        <p class="pop">Link copied to clipboard!</p>
        {/if}
        <h4>
          <a
            href={`${generatedLink}`}
            target="_blank"
            rel="noopener noreferrer"
            id="myInput"
            on:click|preventDefault={copyContent}
          >
            {`${generatedLink}`}
          </a>
        </h4>
      </article>
    </dialog>
  {/if}
</div>

<style lang="scss">
  .pop {
    border-radius: 5px;
    background-color: var(--primary);
    color: var(--primary-inverse);
    padding: 1rem;
    transition: ease-in-out;
  }

// import some colors from pico _colors.scss

</style>
