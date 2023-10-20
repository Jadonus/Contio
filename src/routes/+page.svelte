<script>
  import "animate.css";

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
      <h1>
        Meeting<br /> Scheduling <br />
        Made<br />
        Simple
      </h1>
      <a href="/schedule">Try it out</a>
    </div>
    <div class="img">
      <img src="/booking.svg" />
    </div>
  </div>
</main>

<style>
  .img {
    order: -1;
    display: none;
    margin: 0 auto;
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
      font-size: 7rem;
    }
    a {
      font-size: 2rem;
      padding: 1rem;
    }
  }
  main {
    background-color: var(--pico-color-violet-500);
    height: 100vh;
    font-family: "Inter", sans-serif;
  }

  span {
    font-weight: bold;
    transition: opacity 2s;
  }

  .s {
    background: red;
  }
</style>
