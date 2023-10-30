<script>
  import "animate.css";
  //HOME PAGE
  import { ChevronsRightIcon } from "svelte-feather-icons";

  import Nav from "./Nav.svelte";
  import Chatbubble from "$lib/chatbubble.svelte";
  import Introduction from "$lib/introduction.svelte";
  import Introfollow from "$lib/introfollow.svelte";
  import End from "$lib/end.svelte";
  import Link from "$lib/link.svelte";
  import Footer from "$lib/footer.svelte";
  let hello = "";
</script>

<main>
  <Nav />
  <div class="cont grid">
    <div>
      <h1>Meeting Scheduling Made Simple</h1>
      <a href="/schedule">Start Scheduling</a>
    </div>
    <div class="img">
      <img src="/booking.svg" />
    </div>
  </div>
</main>
<div class="custom-shape-divider-bottom-1697815925">
  <svg
    data-name="Layer 1"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 1200 120"
    preserveAspectRatio="none"
  >
    <path
      d="M0,0V5.63C149.93,59,314.09,71.32,475.83,42.57c43-7.64,84.23-20.12,127.61-26.46,59-8.63,112.48,12.24,165.56,35.4C827.93,77.22,886,95.24,951.2,90c86.53-7,172.46-45.71,248.8-84.81V0Z"
      class="shape-fill"
    />
  </svg>
  <div class="cont">
    <h1 class="sm">Contio is a free app for you to schedule your events.</h1>
    <p>
      From Your kid's birthday party to a work or school meeting, Contio can
      help you figure out people's availibility.
    </p>
    <hr />
    <h1 class="sm sum">Ok, but how does Contio Work</h1>
    <article>
      I'm glad you asked! Contio is very simple at it's core. You (being the
      meeting scheduler) pick a couple dates and times when you are availible,
      then Contio generates a link for you. You then send this link to whoever
      you are inviting. The people receiving this link pick the date and time
      they are availible, and thats it! After A period of time of your choosing,
      and email will be sent to you with the responses.
    </article>
    <h1 class=" sm sum">FAQS</h1>
    <article>
      <details>
        <summary>Do I need to sign up to use Contio?</summary>
        No! Contio is completely free, with no sign ups anywhere.
      </details>
      <hr />

      <details>
        <summary>Will you send me spam?</summary>
        No, your emails are used for your response information, not for advertising
        to you.
      </details>
      <hr />
    </article>
  </div>
</div>
<Footer />

<style>
  .sum {
    margin-top: 2em;
  }
  article {
    border-radius: 20px;
  }
  .img {
    order: -1;
    display: none;
    margin: 0 auto;
  }
  .custom-shape-divider-bottom-1697815925 .shape-fill {
    fill: #9061ca;
  }
  p {
    font-size: 1.5rem;
  }
  footer {
    background-color: var(--pico-color-violet-500);
    width: 100%;
  }
  summary,
  details {
    font-size: 1.2rem;
    margin: 0 0.5rem;
  }
  a {
    background: var(--pico-primary);
    border-radius: 5rem;
    padding: 15px;
    margin: 0.5rem;
    color: var(--pico-text-color);
  }
  h1 {
    font-size: 4.3rem;
    margin-top: 2rem;
    margin-left: 0.5rem;
  }
  @media screen and (min-width: 900px) {
    .cont {
      margin: 0 5rem;
    }
    .img {
      display: block;
      order: 1;
      margin-top: 8em;
    }
    h1 {
      font-size: 5rem;
    }
    a {
      font-size: 1.5rem;
      padding: 0.7rem;
    }
  }
  main {
    background-color: var(--pico-color-violet-500);
    height: 100vh;
    font-family: "Inter", sans-serif;
  }
  .sm {
    font-size: 3rem;
  }
</style>
