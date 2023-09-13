<script>
  import { onMount } from "svelte";

  let zoomScale = 1; // Initial zoom scale
  let backgroundColorOpacity = 0; // Initial background opacity
  let isCentered = false; // Flag to check if the element is centered

  onMount(() => {
    const h1Element = document.querySelector(".textcen");
  const mainElement = document.querySelector("main"); // Select the <main> element

    const handleScroll = () => {
      const elementRect = h1Element.getBoundingClientRect();
      const viewportHeight = window.innerHeight;

      // Calculate the center of the viewport
      const viewportCenter = viewportHeight / 3;

      // Calculate the top and bottom positions of the element
      const elementTop = elementRect.top;
      const elementBottom = elementRect.bottom;

      // Check if the element is in the center of the viewport
      isCentered =
        elementTop <= viewportCenter && elementBottom >= viewportCenter;

      // Calculate the zoom scale based on the element's position
       if (isCentered) {
    zoomScale = 1 + (viewportCenter - elementTop) * 0.08;
    // Adjust this factor as needed

    // But let's make it disappear when it's out of view
    if (elementTop < 0 || elementBottom > viewportHeight) {
      backgroundColorOpacity = 0; // Make it disappear
    } else {
      backgroundColorOpacity = (elementTop - viewportCenter) / viewportCenter;
      // Adjust the opacity range as needed
    }
  } else {
    backgroundColorOpacity = 0; // Not centered, so no need to show it
  }
};
    window.addEventListener("scroll", handleScroll);
  });
</script>

<main>
  <h1 class="textcen">
    Introducing Contio, The easy-to-use scheduling app for groups of <span
      class="primary"
      style="transform: scale({zoomScale});">all</span
    > sizes.
  </h1>
</main>

<style>
  .primary {
    color: var(--pico-primary);
    display: inline-block;
    transform-origin: center;
    transition: transform 0.2s ease;
  }

  .textcen {
    text-align: center;
    height: 100vh; /* Ensure the content takes up the full viewport height */
    margin: 0; /* Remove margin for the h1 element */
  }


</style>
