<script>
  import { ArrowRight } from "phosphor-svelte";
</script>

<a class="hover" href="/schedule" role="button"
  >Start Scheduling <ArrowRight /></a
>

<style>
  .hover:hover {
    background-color: var(--pico-color-violet-500);
    border: 0px;
    scale: 1.1;
    transition: ease-in-out, 0.5s;
  }
  .hover {
    transition: ease-in-out, 0.5s;
  }
</style>
