<script>
  import * as THREE from "three";
  import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
  import SplineLoader from "@splinetool/loader";
  import { onMount } from "svelte";
  // camera

  onMount(() => {
    // camera
    const camera = new THREE.OrthographicCamera(
      window.innerWidth / -2,
      window.innerWidth / 2,
      window.innerHeight / 2,
      window.innerHeight / -2,
      -50000,
      10000
    );
    camera.position.set(0, 0, 0);
    camera.quaternion.setFromEuler(new THREE.Euler(0, 0, 0));

    // scene
    const scene = new THREE.Scene();

    // spline scene
    const loader = new SplineLoader();
    loader.load(
      "https://prod.spline.design/J5NONTcTO6sOd7mF/scene.splinecode",
      (splineScene) => {
        scene.add(splineScene);
      }
    );

    // renderer
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setAnimationLoop(animate);
    document.body.appendChild(renderer.domElement);

    // scene settings
    renderer.shadowMap.enabled = true;
    renderer.shadowMap.type = THREE.PCFShadowMap;

    scene.background = new THREE.Color("#131715");
    renderer.setClearAlpha(1);

    // orbit controls
    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.enableZoom = false; // Disable zooming on scroll

    let spinCount = 0;
    const totalSpins = 2;



      if (spinCount < totalSpins) {
        // Rotate the camera around the target based on the scroll direction
        controls.target.applyAxisAngle(
          new THREE.Vector3(0, 1, 0),
          event.deltaY * 0.001
        );

        // Increment the spin count
        spinCount += event.deltaY;
      } else {
        // If the model has completed a full revolution, enable zooming
      }
    // Add the custom event listener
    document.addEventListener("wheel", onDocumentMouseWheel, false);

    window.addEventListener("resize", onWindowResize);
    function onWindowResize() {
      camera.left = window.innerWidth / -2;
      camera.right = window.innerWidth / 2;
      camera.top = window.innerHeight / 2;
      camera.bottom = window.innerHeight / -2;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    }

    function animate(time) {
      controls.update();
      renderer.render(scene, camera);
    }
  });
</script>
