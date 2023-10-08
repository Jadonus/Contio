<script>
  import Nav from "../Nav.svelte";
  import { onMount } from "svelte";
  import { writable, derived } from "svelte/store";
  import { Trash } from "phosphor-svelte";
  import autoAnimate from '@formkit/auto-animate';

  // Array to store the submitted dates
  let submittedDates = writable([]);
  let formattedDates = derived(submittedDates, ($submittedDates) => {
    return $submittedDates.map((date) => formatDateTime(date));
  });

  let generatedLink = "";
  // Function to handle date submission
  function submitDate(event) {
    const selectedDateTime = event.target.value;

    // Check if the input is not empty and not the default empty value
    if (selectedDateTime && selectedDateTime !== "1970-01-01T00:00") {
      submittedDates.update((dates) => {
        return [...dates, selectedDateTime]; // Update the submittedDates store
      });

      // Format the newly submitted date and add it to the formattedDates array
      const formattedDate = formatDateTime(selectedDateTime);
      formattedDates.update((dates) => {
        return [...dates, formattedDate]; // Update the formattedDates store
      });

      event.target.value = ""; // Clear the input after adding
    }
  }

  function removeDate(date) {
    submittedDates.update((dates) => {
      const index = dates.indexOf(date);
      if (index !== -1) {
        dates.splice(index, 1);
      }
      return [...dates]; // Return a new array to trigger reactivity
    });
  }

  function formatDateTime(dateTimeString) {
    const options = {
      year: "numeric",
      month: "long",
      day: "numeric",
      hour: "numeric",
      minute: "numeric",
    };
    const dateTime = new Date(dateTimeString);
    return dateTime.toLocaleString("en-US", options);
  }

  let dateInput;
  onMount(() => {
    dateInput = document.querySelector('input[type="datetime-local"]');
    dateInput.min = new Date().toISOString().slice(0, 16);
    dateInput.addEventListener("blur", submitDate);
  });

  // Function to generate a random string
  const randomWords = [
    "advertise",
    "arise",
    "afford",
    "assumption",
    "album",
    "ample",
    "agile",
    "attract",
    "approach",
    "aquarium",
    "adviser",
    "aviation",
    "automatic",
    "appear",
    "applied",
    "abuse",
    "adult",
    "amuse",
    "architect",
    "archive",
    "artist",
    "articulate",
    "arrange",
    "arm",
    "addition",
    "arrangement",
    "astonishing",
    "absolute",
    "arrogant",
    "at",
    "apparatus",
    "activate",
    "aware",
    "accident",
    "admission",
    "asset",
    "appendix",
    "appointment",
    "abundant",
    "avenue",
    "annual",
    "apathy",
    "adopt",
    "analysis",
    "amputate",
    "attitude",
    "advantage",
    "aluminium",
    "acceptance",
    "accompany",
  ];

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

  let range=2
  async function makePostRequest(data) {
    try {
      const response = await fetch(
        "https://contio-backend.vercel.app/meeting/submit/new",
        {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(data),
        }
      );

      if (response.ok) {
        console.log("POST request successful!");
      } else {
        console.error("POST request failed!");
      }
    } catch (error) {
      console.error("Error while making POST request:", error);
    }
  }
  let email = "";
  // Inside your generateLink function, after generating the link:
  function generateLink() {
    const randomString = generateRandomString(3);
    const dateParams = $submittedDates.map((date) => `date=${date}`).join("&");
    let now = new Date(); // Get the current date and time
    now.setDate(now.getDate() + range); // Add 2 days to it

const time = now.toISOString(); // 
    const link = `https://contio.vercel.app/schedule/${randomString}?${dateParams}&${time}`;
    generatedLink = link; // Store the link for display
    generatedLinkText = generatedLink;

    last = false 
    // Now, let's create the data to send to your backend
    const postData = {
      timeOfRequest: new Date().toISOString(),
      generatedLink: generatedLink,
      email: email,
      sentime: range,
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
  function share() {
    if (navigator.share) {
      navigator
        .share({
          url: generatedLinkText,
        })
        .then(() => console.log("Successful share"))
        .catch((error) => console.log("Error sharing", error));
    } else {
      const copyContent = async () => {
        try {
          await navigator.clipboard.writeText(generatedLinkText);
          console.log("Content copied to clipboard");
          pop = true;
        } catch (err) {
          console.error("Failed to copy: ", err);
        }
      };
      copyContent();
    }
  }
  let last = false
  function lastmod() {
    last = true
  }
</script>

<Nav />
<header class="container">
  <hgroup>
    <h1>When are you available?</h1>
    <h2>Pick a couple times when you are available to meet.</h2>
  </hgroup>
  <div class="grid">
    <div>
      <input
        type="datetime-local"
        min={new Date().toISOString().slice(0, 16)}
      />
    </div>

    <div>
      <input type="email" bind:value={email} placeholder="Your Email." />
    </div>
  </div>
</header>

<div class="container">
  <ul use:autoAnimate>
    {#each $submittedDates as date (date)}
      <!-- Use submittedDates instead of formattedDates -->
      <li>
        {formatDateTime(date)}
        <!-- Format the date here directly -->
        <button class="trash" on:click={() => removeDate(date)}
          ><Trash size="1.3rem" /></button
        >
      </li>
    {/each}
  </ul>
  <div class="grid">
    <button
      on:click={lastmod}
      disabled={!$submittedDates.length || !email.length}>Continue</button
    >
  </div>
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
            on:click|preventDefault={share}
          >
            {`${generatedLink}`}
          </a>
        </h4>
      </article>
    </dialog>
  {/if}
 {#if last}
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
          <h2>Last Step!</h2>
        </header>
        <h4>
        How long should you wait until the responses are sent to you?

        </h4>
        <input type="range" min="1" bind:value={range}/>
        <p>{range} day(s)</p>
        <div class="grid">
        <button on:click={generateLink}>Generate My Link!</button>
        </div>
      </article>
    </dialog>
  {/if}
</div>

<style lang="scss">
  .trash {
    padding: 0.2rem;
    border-color: var(--pico-color-violet-500);
    border-radius: 50%;
    background-color: var(--pico-color-violet-500);

    font-smooth: auto;
  }
  .pop {
    border-radius: 5px;
    background-color: var(--primary);
    color: var(--primary-inverse);
    padding: 1rem;
    transition: ease-in-out;
  }
  .center {
    display: flex;
    justify-items: center;
    align-items: center;
  }
  main {
    font-family: "Inter", sans-serif;

    --pico-font-family: "Inter", sans-serif;
  }
</style>
