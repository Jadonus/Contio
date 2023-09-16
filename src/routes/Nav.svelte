<script>
  import { redirect } from "@sveltejs/kit";
</script>

<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/@picocss/pico@next/css/pico.min.css"
/>
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/@picocss/pico@next/css/pico.colors.min.css"
/>
<link rel="preconnect" href="https://fonts.googleapis.com"> 
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin> 
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@500&display=swap" rel="stylesheet">

<html lang="html">
  <div class="hero">
    <nav class="">
      <ul>
        <li>
          <strong
            ><a class="white" href="/"
              >Contio <svg
                xmlns="http://www.w3.org/2000/svg"
                height="1em"
                viewBox="0 0 512 512"
                ><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path
                  d="M240.1 4.2c9.8-5.6 21.9-5.6 31.8 0l171.8 98.1L448 104l0 .9 47.9 27.4c12.6 7.2 18.8 22 15.1 36s-16.4 23.8-30.9 23.8H32c-14.5 0-27.2-9.8-30.9-23.8s2.5-28.8 15.1-36L64 104.9V104l4.4-1.6L240.1 4.2zM64 224h64V416h40V224h64V416h48V224h64V416h40V224h64V420.3c.6 .3 1.2 .7 1.8 1.1l48 32c11.7 7.8 17 22.4 12.9 35.9S494.1 512 480 512H32c-14.1 0-26.5-9.2-30.6-22.7s1.1-28.1 12.9-35.9l48-32c.6-.4 1.2-.7 1.8-1.1V224z"
                /></svg
              ></a
            ></strong
          >
        </li>
      </ul>
      <ul>
        <li><a class="white" href="#">Link</a></li>
        <li><a class="mr white" href="#">Link</a></li>
      </ul>
    </nav>
  </div>
  <style>
    html {
    overflow-x: hidden;
    underline-color: purple;
    -webkit::overflow-x: hidden;
    }
    .white {
      margin-left: 5px;
    }
    .mr {
      margin-right: 10px;
    }
    a:hover {
    }
    html {
      max-width: 100%;
      overflow-x: hidden;
      font-family:  'Inter', sans-serif;
      --pico-font-family: 'Inter', sans-serif;
    }
    ::-webkit-scrollbar {
      display: none;
    }
    /* Orange color for light color scheme (Default) */
    /* Can be forced with data-theme="light" */
    [data-theme="light"],
    :root:not([data-theme="dark"]) {
      --pico-text-selection-color: rgba(244, 93, 44, 0.25);
      --pico-primary: #bd3c13;
      --pico-primary-background: #d24317;
      --pico-primary-underline: rgba(189, 60, 19, 0.5);
      --pico-primary-hover: #942d0d;
      --pico-primary-hover-background: #bd3c13;
      --pico-primary-focus: rgba(244, 93, 44, 0.25);
      --pico-primary-inverse: #fff;
    }

    /* Orange color for dark color scheme (Auto) */
    /* Automatically enabled if user has Dark mode enabled */
    @media only screen and (prefers-color-scheme: dark) {
      :root:not([data-theme]) {
        --pico-text-selection-color: rgba(245, 107, 61, 0.1875);
        --pico-primary: #f56b3d;
        --pico-color: #fff;

        --pico-primary-background: #d24317;
        --pico-primary-underline: rgba(245, 107, 61, 0.5);
        --pico-primary-hover: #f8a283;
        --pico-primary-hover-background: #e74b1a;
        --pico-primary-focus: rgba(245, 107, 61, 0.25);
        --pico-primary-inverse: #fff;
      }
    }

    /* Orange color for dark color scheme (Forced) */
    /* Enabled if forced with data-theme="dark" */
    [data-theme="dark"] {
      --pico-text-selection-color: rgba(245, 107, 61, 0.1875);
      --pico-primary: #f56b3d;

      --pico-color: #000000;
      --pico-primary-background: #d24317;
      --pico-primary-underline: rgba(245, 107, 61, 0.5);
      --pico-primary-hover: #f8a283;
      --pico-primary-hover-background: #e74b1a;
      --pico-primary-focus: rgba(245, 107, 61, 0.25);
      --pico-primary-inverse: #fff;
    }
    .white {
      color: var(--pico-background);

    text-decoration-color: var(--pico-color-violet-500);
    }
  </style>
</html>
