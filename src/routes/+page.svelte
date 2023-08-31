<script>
import 'animate.css';

import Nav from './Nav.svelte'
    let hello =""
</script>

<Nav />
<header class="container">
        <hgroup>
          <h1 class="animate__animated animate__bounceInLeft">Contio</h1>
          <h2 class="larger ">Lets Meet up.</h2>
        </hgroup>
        <p><a href="/schedule" role="button" >Start Scheduling</a></p>
      </header>
<style>

h1 {
    font-size: 7em
}
.larger {
    font-size: 2em
}

</style>
