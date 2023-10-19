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
  <div class="h">
    <Nav />

    <header class="container mt">
      <hgroup class="grid">
        <div>
          <h1 class="he" data-aos="zoom-in-right">Contio</h1>
          <h2 class="larger" data-aos="zoom-in-right">Let's Meet up.</h2>
          <Link />
        </div>
        <div class="image-container" />
      </hgroup>
      <div class="vh" />

      <Chatbubble />
    </header>

    <Introduction />

    <Introfollow />
    <End />
  </div>

  <Footer />
</main>

<style>
  .he {
    font-size: 10em;
  }
  .h {
    overflow-x: hidden;
    -webkit-overflow-scrolling: touch;
  }
  h1 {
    font-size: 6em;

    font-weight: bolder;
    font-family: "Inter", sans-serif;
  }
  .larger {
    font-size: 2em;

    font-family: "Inter", sans-serif;
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
    .he {
      font-size: 7em;
      margin-top: 1em;
    }
    .grid {
      flex-direction: column;
      text-align: center;
    }

    .image-container {
      order: -1;
      margin-left: 5em;
      background-size: cover;
      margin-right: 5em;
    }
  }
  img {
  }
  .mt {
    margin-top: 4em;
  }
  .h {
    background-image: url("cri.svg");
    background-size: cover;
  }
  .vh {
    padding-top: 75vh;
  }
</style>
