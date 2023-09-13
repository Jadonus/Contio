<script>
  import "animate.css";
  import { ChevronsRightIcon } from "svelte-feather-icons";

  import Nav from "./Nav.svelte";
  import Chatbubble from "$lib/chatbubble.svelte";
  import Introduction from "$lib/introduction.svelte";
  
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
    <Introduction />
  </header>

  <div class="wh center" style="background-color:var(--pico-primary)">
    <h2 class="text-center">
      Contio is designed with simplicity and ease of use in mind.
    </h2>
  </div>
  <div class="custom-shape-divider-top-1694565909">
    <svg
      data-name="Layer 1"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 1200 120"
      preserveAspectRatio="none"
    >
      <path
        d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V0H0V27.35A600.21,600.21,0,0,0,321.39,56.44Z"
        class="shape-fill"
      />
    </svg>
  </div>
</main>

<style>
  .custom-shape-divider-top-1694565909 .shape-fill {
    fill: var(--pico-primary);
  }
  .text-center {
    text-align: center;
  }
  .center {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .wh {
    width: 100vw;
    height: 100vh;
    padding: 0;
    margin: 0;
  }
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
  .pad {
    margin-top: 20em;
  }
  .mt {
    margin-top: 4em;
  }
  .vh {
    padding-top: 75vh;
  }
</style>
