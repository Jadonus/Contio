<script>
  import { onMount } from "svelte";
  onMount(() => {
    AOS.init();
    function parallax() {
      var s = document.getElementById("floater");

      var s2 = document.getElementById("floater2");
      var yPos = 0 - window.pageYOffset / 8;
      s.style.top = 200 + yPos + "%";

      s2.style.top = 380 + yPos + "%";
    }

    window.addEventListener("scroll", function () {
      parallax();
    });
  });
</script>

<main>
  <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet" />
  <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>

  <div
    data-aos="fade-right"
    class="talk-bubble tri-right round btm-left"
    style="float: left;"
  >
    <div class="talktext">
      <p class="">
        Have you ever needed to <br />schedule a meeting with<br /> several
        people, all <br />with different availibility?
      </p>
    </div>
  </div>
  <svg
    id="floater"
    class="float-center"
    style="height: 50vh; width: 50vw;float: right"
    viewBox="0 0 200 200"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      fill="#D24318"
      d="M42.1,-56.3C51.7,-42,54.9,-26.1,54.3,-12.2C53.6,1.7,49,13.7,43.4,26.8C37.9,39.9,31.4,54.2,20.4,59.8C9.4,65.5,-6.1,62.5,-22.3,58C-38.5,53.5,-55.3,47.6,-65.1,35.3C-74.9,23,-77.7,4.4,-75.9,-14.7C-74.1,-33.8,-67.7,-53.5,-54.3,-67.1C-40.9,-80.8,-20.4,-88.4,-2.1,-85.9C16.2,-83.3,32.4,-70.6,42.1,-56.3Z"
      transform="translate(100 100)"
    />
  </svg>
  <div class="padb" />
  <div
    data-aos="fade-left"
    class="talk-bubble tri-right round btm-right"
    style="float: right;"
  >
    <div class="talktext">
      <p class="">
     Yep, its a pain.   
      </p>
    </div>
  </div>
  <svg
    id="floater2"
    class="float-center2"
    style="height: 50vh; width: 50vw;float: right"
    viewBox="0 0 200 200"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      fill="#D24318"
      d="M42.1,-56.3C51.7,-42,54.9,-26.1,54.3,-12.2C53.6,1.7,49,13.7,43.4,26.8C37.9,39.9,31.4,54.2,20.4,59.8C9.4,65.5,-6.1,62.5,-22.3,58C-38.5,53.5,-55.3,47.6,-65.1,35.3C-74.9,23,-77.7,4.4,-75.9,-14.7C-74.1,-33.8,-67.7,-53.5,-54.3,-67.1C-40.9,-80.8,-20.4,-88.4,-2.1,-85.9C16.2,-83.3,32.4,-70.6,42.1,-56.3Z"
      transform="translate(100 100)"
    />
  </svg>
  <div class="padb" />
</main>

<style>
  /* General CSS Setup */
main {
  font-size: 2rem;
}
 

/* container */
  /* CSS talk bubble */
  .float-center {
    position: absolute;
    top: 200%;
    margin-top: 50vh;
  }
  .float-center2 {
    position: absolute;
    top: 380%;
    margin-top: 50vh;
  }

  .padb {
    padding-bottom: 100vh;
  }
</style>
