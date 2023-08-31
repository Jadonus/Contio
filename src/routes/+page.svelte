<script>
import 'animate.css';
  import { ChevronsRightIcon} from 'svelte-feather-icons'

import Nav from './Nav.svelte'
    let hello =""
</script>

<Nav />
<header class="container">
        <hgroup>
          <h1 class="animate__animated animate__bounceInLeft">Contio</h1>
          <h2 class="larger ">Lets Meet up.</h2>
        </hgroup>
        <p><a href="/schedule" class="link-arrow" role="button" >Start Scheduling <p><ChevronsRightIcon /></p> </a></p>
<article class="mdt">
  <header><h3>What even is Contio?</h3></header>
  Good question! Contio is a meeting 
  scheduling app, designed for simplicity for both you and the person who are meeting with.
   Nice! 👍 In case you're wondering, Contio means 'meeting', or 'assembly' in latin. 
</article>

      </header>
<style>

h1 {
    font-size: 7em
}
.larger {
    font-size: 2em
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
.mdt {
  margin-top: 20em;
}
</style>
