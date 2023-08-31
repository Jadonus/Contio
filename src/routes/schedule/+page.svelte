<script>
  import Nav from "../Nav.svelte";
  import { onMount } from "svelte";

  // Array to store the submitted dates
  let submittedDates = [];
  let generatedLink = "";

  // Function to handle date submission
  function submitDate(event) {
    const selectedDateTime = event.target.value;
    if (selectedDateTime && !submittedDates.includes(selectedDateTime)) {
      submittedDates = [...submittedDates, selectedDateTime];
    }
  }

  onMount(() => {
    const dateInput = document.querySelector('input[type="datetime-local"]');
    dateInput.addEventListener("change", submitDate);
  });

  // Function to generate a random string
  const randomWords = [
    "Siamese",
    "Unaired",
    "Kindness",
    "Scary",
    "Unshipped",
    "Epilepsy",
    "Sandblast",
    "Closure",
    "Devouring",
    "Litter",
    "Clad",
    "Backfire",
    "Squishy",
    "Thursday",
    "Grope",
    "Unhearing",
    "Rise",
    "Steersman",
    "Parchment",
    "Spinster",
    "Glamorous",
    "Either",
    "Autism",
    "Lapdog",
    "Exposure",
    "Doorstep",
    "Nerd",
    "Slashed",
    "Rotting",
    "Submersed",
    "Dismount",
    "Surprise",
    "Duo",
    "Easel",
    "Dose",
    "Frostily",
    "Unexposed",
    "Ammonium",
    "Unguarded",
    "Botch",
    "Varmint",
    "Petite",
    "Track",
    "Posting",
    "Armband",
    "Amicably",
    "Blaspheme",
    "Stylized",
    "Blurry",
    "Colossal",
    "Quarry",
    "Plant",
    "Humbly",
    "Jeep",
    "Parched",
    "Bulb",
    "Litmus",
    "Unbalance",
    "Trash",
    "Faculty",
    "Woven",
    "Limes",
    "Gladly",
    "Map",
    "Willed",
    "Backlit",
    "Papyrus",
    "Playhouse",
    "Unfailing",
    "Ancient",
    "Capital",
    "Bobtail",
    "Election",
    "Jackpot",
    "Rental",
    "Stoic",
    "Revisit",
    "Snub",
    "Everyday",
    "Crystal",
    "Mobster",
    "Chamber",
    "Careless",
    "Device",
    "Neurotic",
    "Emerald",
    "Disabled",
    "Maximum",
    "Reviving",
    "Unearned",
    "Phantom",
    "Footwork",
    "Cruncher",
    "Disallow",
    "Steed",
    "Supermom",
    "Shifter",
    "Panther",
    "Cofounder",
    "Anime",
    "Exfoliate",
    "Backtrack",
    "Runaround",
    "Undoing",
    "Projector",
    "Canary",
    "Irate",
    "Registry",
    "Amaze",
    "Empty",
    "Curing",
    "Overstate",
    "Decent",
    "Trunks",
    "Praising",
    "Oblong",
    "Playtime",
    "Aflame",
    "Compile",
    "Underfoot",
    "Aftermost",
    "Until",
    "Dice",
    "Paternal",
    "Tycoon",
    "Yonder",
    "Embezzle",
    "Player",
    "Gradient",
    "Driver",
    "Deviancy",
    "Regulate",
    "Scale",
    "Epilogue",
    "Uncross",
    "Acid",
    "Spree",
    "Backstage",
    "Manor",
    "Underfoot",
    "Brute",
    "French",
    "Crummiest",
    "Boney",
    "Drainage",
    "Spotted",
    "Unframed",
    "Flashcard",
    "Glimmer",
    "Bacteria",
    "Tremor",
    "Unripe",
    "Outreach",
    "Rumble",
    "Starting",
    "Encore",
    "Entrust",
    "Shrapnel",
    "Overtime",
    "Wriggly",
    "Eligible",
    "Velcro",
    "Handed",
    "Manned",
    "Scarily",
    "Handling",
    "Agony",
    "Catwalk",
    "Reaffirm",
    "Scroll",
    "Handcraft",
    "Stinging",
    "Duckbill",
    "Penholder",
    "Escapade",
    "Vitally",
    "Sapling",
    "Immodest",
    "Senate",
    "Scaling",
    "Fiddle",
    "Ascension",
    "Felt-tip",
    "Handheld",
    "Valid",
    "Mortally",
    "Facedown",
    "Spud",
    "Antitoxic",
    "Defuse",
    "Ferret",
    "Ninetieth",
    "Quilt",
    "Overhead",
    "Removal",
    "Guiding",
    "Wound",
    "Expire",
    "Impose",
    "Reorder",
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

  function generateLink() {
    const randomString = generateRandomString(3);
    const dateParams = submittedDates.map((date) => `date=${date}`).join("&");
    const link = `https://contio.vercel.app/schedule/${randomString}?${dateParams}`;
    generatedLink = link; // Store the link for display
     generatedLinkText = generatedLink;

  }

  // Function to close the modal
  function closeModal() {
    const modal = document.querySelector("dialog[open]");
    if (modal) {
      modal.removeAttribute("open");
    }
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
  let formatedDateTime = [];
  let orgiginalDateTime = "0";
  let originalDateTime;
  const formattedDateTime = formatDateTime(originalDateTime);
  console.log(formattedDateTime);
  
  
let pop = false
  const copyContent = async () => {
    try {
      await navigator.clipboard.writeText(generatedLinkText);
      console.log('Content copied to clipboard');
      pop = true
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
  <input type="datetime-local" />
</header>

<div class="container">
  <ul>
    {#each submittedDates as date}
      <li>{date}</li>
    {/each}
  </ul>

  <button role="button" on:click={generateLink}>Generate link from dates</button
  >

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

<style>
  .pop {
    border-radius: 5px;
    background-color: var(--primary);
    color: var(--primary-inverse);
    padding: 1rem;
    transition: ease-in-out;
  }
</style>
