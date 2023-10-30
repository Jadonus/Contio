<script>
  //MEETING CREATION PAGE
  import Nav from "../Nav.svelte";
  import { onMount } from "svelte";
  import { writable, derived } from "svelte/store";
  import { Trash } from "phosphor-svelte";
  import autoAnimate from "@formkit/auto-animate";
  let admilink = "";
  let submittedDates = writable([]);
  let formattedDates = derived(submittedDates, ($submittedDates) => {
    return $submittedDates.map((date) => formatDateTime(date));
  });

  let generatedLink = "";
  function submitDate(event) {
    const selectedDateTime = event.target.value;

    if (selectedDateTime && selectedDateTime !== "1970-01-01T00:00") {
      submittedDates.update((dates) => {
        return [...dates, selectedDateTime];
      });

      const formattedDate = formatDateTime(selectedDateTime);
      formattedDates.update((dates) => {
        return [...dates, formattedDate];
      });

      event.target.value = "";
    }
  }

  function removeDate(date) {
    submittedDates.update((dates) => {
      const index = dates.indexOf(date);
      if (index !== -1) {
        dates.splice(index, 1);
      }
      return [...dates];
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

  function generateRandomString(length) {
    let result = "";
    for (let i = 0; i < length; i++) {
      const randomIndex = Math.floor(Math.random() * randomWords.length);
      result += randomWords[randomIndex];
    }
    return result;
  }

  let generatedLinkText = "";

  let range = 2;
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
  let runad = false;
  console.log(runad);
  function admin() {
    const encodedLink = generatedLink.replace(/&/g, "%26");
    let r = (Math.random() + 1).toString(36).substring(7);
    admilink = `https://contio.vercel.app/admin/${r}?link=${encodedLink}`;
    console.log(admilink);
  }

  function toggleAdmin() {
    if (runad) {
      admin();
    } else {
      console.log("Admin function is not enabled.");
    }
  }
  function generateLink() {
    const randomString = generateRandomString(3);
    const dateParams = $submittedDates.map((date) => `date=${date}`).join("&");
    let now = new Date();
    now.setDate(now.getDate() + range);
    console.log(now);
    const time = now.toISOString();
    const link = `https://contio.vercel.app/schedule/${randomString}?${dateParams}&time=${time}`;
    generatedLink = link;
    generatedLinkText = generatedLink;
    toggleAdmin();
    last = false;
    const postData = {
      timeOfRequest: new Date().toISOString(),
      generatedLink: generatedLink,
      email: email,
      sentime: range,
    };

    makePostRequest(postData);
  }

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
  let last = false;
  function lastmod() {
    last = true;
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
        placeholder="Pick Some dates."
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
        {#if runad}
          <p>Admin Page Link (Don't share this)</p>
          <h4>
            <a
              href={admilink}
              target="_blank"
              rel="noopener noreferrer"
              id="myInput"
            >
              {admilink}
            </a>
          </h4>
        {/if}
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
        <h4>How long should you wait until the responses are sent to you?</h4>
        <input type="range" min="1" bind:value={range} />
        <p>{range} day(s)</p>
        <h4>
          Should The Admin Dashboard Feature Be enabled? <a href="/admin/"
            >info</a
          >
        </h4>
        <input name="check" class="mb" type="checkbox" bind:checked={runad} />
        <label for="check">Enable it!</label>
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
  .mb {
    margin-bottom: 1rem;
  }
  dialog[open] {
    overflow: auto;
  }
</style>
