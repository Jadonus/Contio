<script>
  import "animate.css";
  import { ChevronsRightIcon } from "svelte-feather-icons";

  import Nav from "./Nav.svelte";
  import Chatbubble from "$lib/chatbubble.svelte";
  import Introduction from "$lib/introduction.svelte";
  import Introfollow from "$lib/introfollow.svelte";
  import End from "$lib/end.svelte";
  let hello = "";
</script>

<main>
  <Nav />
  <header class="container mt">
    <hgroup class="grid">
      <div>
        <h1 class="animate__animated animate__bounceInLeft">Contio</h1>
        <h2 class="larger">Let's Meet up.</h2>
        <a href="/schedule" class="link-arrow" role="button">
          Start Scheduling <p><ChevronsRightIcon /></p>
        </a>
      </div>
      <div class="image-container">
        <img class="" alt="meeting" src="meeting2.svg" />
      </div>
    </hgroup>
    <div class="vh" />

    <Chatbubble />
  </header>

    <Introduction />

    <Introfollow />
<End />
</main>
<style>
 
  h1 {
    font-size: 6.5em;

    font-family: sans-serif;
  }
  .larger {
    font-size: 2em;

    font-family: sans-serif;
  }
  a {
    text-decoration: none;
  }

  .link-arrow p {
    display: inline-block;
    transition: 0.1s ease-in;

    margin-bottom: -10px;
  }
  .link-arrow:hover p {
    transform: translateX(50%);
  }

  @media (max-width: 768px) {
    .grid {
      flex-direction: column;
      text-align: center;
    }

    .image-container {
      order: -1;
      margin-left: 50px;

      margin-right: 50px;
    }
  }
  
  .mt {
    margin-top: 4em;
  }
  .vh {
    padding-top: 75vh;
  }
</style>
