<script>
  import Rellax from "rellax";
  import { onMount } from "svelte";
  onMount(() => {
    const rellax = new Rellax(".rellax");
  });

  /* import * as THREE from "three";
  import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";

  let model; // Define the model variable

  import { onMount } from "svelte";
  onMount(() => {
    // Set up your scene, camera, and renderer as usual
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const ambientLight = new THREE.AmbientLight(0xffffff, 1); // Adjust intensity as needed
    scene.add(ambientLight);

    // Create a container div for the renderer
    const rendererContainer = document.createElement("div");
    rendererContainer.style.position = "absolute"; // Position it as needed
    rendererContainer.style.top = "215%"; // Adjust the vertical position
    rendererContainer.style.left = "-100px"; // Adjust the horizontal position
    rendererContainer.style.width = "1em"; // Set the desired width

    rendererContainer.setAttribute("data-aos", "fade-left");
    rendererContainer.style.float = "right"; 

    rendererContainer.style.height = "1em";
    document.body.appendChild(rendererContainer);

    const renderer = new THREE.WebGLRenderer({ alpha: true }); // Add { alpha: true }
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setClearColor(0x000000, 0); // Set clear color to transparent
    rendererContainer.appendChild(renderer.domElement); // Append renderer to the container

    // Load the GLTF model
    const loader = new GLTFLoader();

    loader.load("/thinking/scene.gltf", (gltf) => {
      model = gltf.scene;

      // Position the model
      model.position.set(0, 0, 0); // Adjust the position as needed

      model.scale.set(0.7, 0.7, 0.7); // This scales the model's height to half while keeping the other dimensions the same
      // Add the model to the scene
      scene.add(model);

      // Position the camera
      camera.position.z = 5;

      // Create an animation loop to make the model spin
      const animate = () => {
        requestAnimationFrame(animate);

        // Rotate the model
        if (model) {
          model.rotation.x += 0.001;
          model.rotation.y += 0.001;
        }

        renderer.render(scene, camera);
      };

      animate();
    });
  });
  onMount(() => {
    let model2;
    // Set up your scene, camera, and renderer as usual
    const scene2 = new THREE.Scene();
    const camera2 = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const ambientLight2 = new THREE.AmbientLight(0xffffff, 1); // Adjust intensity as needed
    scene2.add(ambientLight2);

    // Create a container div for the renderer
    const rendererContainer2 = document.createElement("div");
    rendererContainer2.style.position = "absolute"; // Position it as needed
    rendererContainer2.style.top = "120%"; // Adjust the vertical position
    rendererContainer2.style.width = "0.5em"; // Set the desired width
    rendererContainer2.setAttribute("data-aos", "fade-left");

    rendererContainer2.style.float = "left"; 
    rendererContainer2.style.height = "1em";
    document.body.appendChild(rendererContainer2);

    const renderer2 = new THREE.WebGLRenderer({ alpha: true }); // Add { alpha: true }
    renderer2.setSize(window.innerWidth, window.innerHeight);
    renderer2.setClearColor(0x000000, 0); // Set clear color to transparent
    rendererContainer2.appendChild(renderer2.domElement); // Append renderer to the container

    // Load the GLTF model
    const loader2 = new GLTFLoader();

    loader2.load("/question/scene.gltf", (gltf) => {
      model2 = gltf.scene;

      // Position the model
      model2.position.set(0, 0, 0); // Adjust the position as needed

      // Add the model to the scene
      scene2.add(model2);

      // Position the camera
      camera2.position.z = 5;

      model2.rotation.x = 2;
      model2.scale.set(0.7, 0.7, 0.7); // This scales the model's height to half while keeping the other dimensions the same

      // Create an animation loop to make the model spin
      const animate2 = () => {
        requestAnimationFrame(animate2);

        // Rotate the model
        if (model2) {
          model2.rotation.x += 0.001;
          model2.rotation.y += 0.001;
        }

        renderer2.render(scene2, camera2);
      };

      animate2();
    });
  });
  */
</script>

<main>
  <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet" />
  <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>

  <div data-aos="fade-right" class="talk-bubble tri-right round btm-left">
    <div class="talktext">
      <p class="rellax" data-rellax-speed="-2">
        Have you ever <br />needed to <br />schedule a<br /> meeting with<br />
        several people, all <br />with different availibility?
      </p>

      <h1
        style="
font-size: 4em;
      "
        class="rellax"
        data-rellax-speed="-1"
      >
        ✏️
      </h1>
    </div>
  </div>

  <div class="padb" />
  <div class="talktext">
    <p data-rellax-speed="2" class="rellax">Yep, its a pain.</p>
    <h1
      style="
font-size: 4em;
    "
      data-rellax-speed="1.2"
      class="rellax"
    >
      🤔
    </h1>
  </div>

  <div class="padb" />
</main>

<style>
  /* General CSS Setup */
  main {
    font-size: 1.5rem;
    font-family: "Inter", sans-serif;
    overflow-x: hidden;
  }

  /* container */
  /* CSS talk bubble */
  .talktext {
    display: flex;
    justify-content: space-around;
    flex-direction: row;
  }
  .padb {
    padding-bottom: 120vh;
  }
</style>
