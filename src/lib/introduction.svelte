<script>
  import { onMount } from "svelte";
  // camera
  onMount(() => {
    AOS.init();
  });
  // camera
</script>

<main class="">
  <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet" />
  <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
  <div data-aos="fade" data-aos-delay="600" data-aos-duration="2000" class="bg">
    <div class="canvas-container" />
    <div class="flex">
      <h1 class="textcen">
        Introducing Contio, The easy-to-use scheduling app for groups of all
        sizes.<br />
        <a role="button" class="tpm link" href="/schedule"
          >Schedule Your Own Meeting</a
        >
      </h1>
    </div>
  </div>
</main>

<style>
  /* Ensure the main element contains the background image */
  /* Ensure the main element contains the background image */
  .bg {
    background-image: linear-gradient(
      35deg,
      hsl(14deg 79% 46%) 6%,
      hsl(13deg 80% 47%) 49%,
      hsl(11deg 80% 48%) 62%,
      hsl(10deg 81% 49%) 70%,
      hsl(8deg 81% 50%) 76%,
      hsl(6deg 84% 51%) 80%,
      hsl(4deg 87% 52%) 84%,
      hsl(2deg 91% 53%) 88%,
      hsl(358deg 96% 53%) 92%,
      hsl(353deg 100% 50%) 100%
    );
  }

  /* Style the canvas container to fill the screen */
  .canvas-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1; /* This is crucial to place it behind the text */
  }

  /* Style the canvas element (Three.js graphic) */
  #webgl-canvas {
    width: 100%;
    height: 100%;
  }

  /* Style the text container */
  .flex {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    position: relative; /* Make it relative */
    z-index: 1; /* Set a higher z-index to keep it above the background color */
  }
  .tpm {
    margin-top: 1rem;
  }

  .textcen {
    text-align: center;
    margin: 0;
  }
</style>
