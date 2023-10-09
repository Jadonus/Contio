<script>
import {page} from '$app/stores'
  import Nav from "../../Nav.svelte";
  import { onMount } from 'svelte';

const slug = $page.params.generatedLink; 
const genlink = $page.url.searchParams.get('link')
  const apiUrl = 'https://contio-backend.vercel.app/meeting/admin/';

 onMount(async () => {
    try {
      const response = await fetch(apiUrl, {
        method: 'POST', // You may need to specify the correct HTTP method (POST, GET, etc.)
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ link: genlink }),
      });

      if (response.ok) {
        const data = await response.json();
        console.log(data);
      } else {
        console.error('Fetch request failed with status:', response.status);
      }
    } catch (error) {
      console.error('Error during fetch:', error);
    }
  });
    </script>
    <main>
<Nav />
<h1>{genlink} </h1>
    </main>