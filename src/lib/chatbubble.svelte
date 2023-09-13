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
        Hey everyone. We need to schedule a meeting. If everyone could send in
        the dates they are availible in the chat, we will get something
        scheduled.
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
        Ok. Who is going to sort through all the answers and compare them? There
        are 20 people attending!
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
  .talk-bubble {
    margin: 40px;
    display: inline-block;
    position: relative;
    width: 200px;
    height: auto;
    background-color: lightgray;
  }
  .border {
    border: 8px solid #666;
  }
  .round {
    border-radius: 30px;
    -webkit-border-radius: 30px;
    -moz-border-radius: 30px;
  }

  /* Right triangle placed top left flush. */
  .tri-right.border.left-top:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: -40px;
    right: auto;
    top: -8px;
    bottom: auto;
    border: 32px solid;
    border-color: #666 transparent transparent transparent;
  }
  .tri-right.left-top:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: -20px;
    right: auto;
    top: 0px;
    bottom: auto;
    border: 22px solid;
    border-color: lightgray transparent transparent transparent;
  }

  /* Right triangle, left side slightly down */
  .tri-right.border.left-in:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: -40px;
    right: auto;
    top: 30px;
    bottom: auto;
    border: 20px solid;
    border-color: #666 #666 transparent transparent;
  }
  .tri-right.left-in:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: -20px;
    right: auto;
    top: 38px;
    bottom: auto;
    border: 12px solid;
    border-color: lightgray lightgray transparent transparent;
  }

  /*Right triangle, placed bottom left side slightly in*/
  .tri-right.border.btm-left:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: -8px;
    right: auto;
    top: auto;
    bottom: -40px;
    border: 32px solid;
    border-color: transparent transparent transparent #666;
  }
  .tri-right.btm-left:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: 0px;
    right: auto;
    top: auto;
    bottom: -20px;
    border: 22px solid;
    border-color: transparent transparent transparent lightgray;
  }

  /*Right triangle, placed bottom left side slightly in*/
  .tri-right.border.btm-left-in:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: 30px;
    right: auto;
    top: auto;
    bottom: -40px;
    border: 20px solid;
    border-color: #666 transparent transparent #666;
  }
  .tri-right.btm-left-in:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: 38px;
    right: auto;
    top: auto;
    bottom: -20px;
    border: 12px solid;
    border-color: lightgray transparent transparent lightgray;
  }

  /*Right triangle, placed bottom right side slightly in*/
  .tri-right.border.btm-right-in:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: 30px;
    bottom: -40px;
    border: 20px solid;
    border-color: #666 #666 transparent transparent;
  }
  .tri-right.btm-right-in:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: 38px;
    bottom: -20px;
    border: 12px solid;
    border-color: lightgray lightgray transparent transparent;
  }
  /*
	left: -8px;
  right: auto;
  top: auto;
	bottom: -40px;
	border: 32px solid;
	border-color: transparent transparent transparent #666;
	left: 0px;
  right: auto;
  top: auto;
	bottom: -20px;
	border: 22px solid;
	border-color: transparent transparent transparent lightgray;

/*Right triangle, placed bottom right side slightly in*/
  .tri-right.border.btm-right:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: -8px;
    bottom: -40px;
    border: 20px solid;
    border-color: #666 #666 transparent transparent;
  }
  .tri-right.btm-right:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: 0px;
    bottom: -20px;
    border: 12px solid;
    border-color: lightgray lightgray transparent transparent;
  }

  /* Right triangle, right side slightly down*/
  .tri-right.border.right-in:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: -40px;
    top: 30px;
    bottom: auto;
    border: 20px solid;
    border-color: #666 transparent transparent #666;
  }
  .tri-right.right-in:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: -20px;
    top: 38px;
    bottom: auto;
    border: 12px solid;
    border-color: lightgray transparent transparent lightgray;
  }

  /* Right triangle placed top right flush. */
  .tri-right.border.right-top:before {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: -40px;
    top: -8px;
    bottom: auto;
    border: 32px solid;
    border-color: lightgray transparent transparent transparent;
  }
  .tri-right.right-top:after {
    content: " ";
    position: absolute;
    width: 0;
    height: 0;
    left: auto;
    right: -20px;
    top: 0px;
    bottom: auto;
    border: 20px solid;
    border-color: lightgray transparent transparent transparent;
  }

  /* talk bubble contents */
  .talktext {
    padding: 1em;
    text-align: left;
    line-height: 1.5em;
  }
  .talktext p {
    /* remove webkit p margins */
    -webkit-margin-before: 0em;
    -webkit-margin-after: 0em;

    color: black;
  }
  .padb {
    padding-bottom: 100vh;
  }
</style>
