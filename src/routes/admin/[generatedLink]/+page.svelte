<script>
  import { page } from "$app/stores";
  import Nav from "../../Nav.svelte";
  import { onMount } from "svelte";
  const genlink = $page.url.searchParams.get("link");

  const slug = $page.params.generatedLink;
  // Get the entire query string
  const apiUrl = "https://contio-backend.vercel.app/meeting/admin/";
  let apistuff;
  let dateData = []; // An array to store the date data for the pie chart
  let pieChart;
  import Chart from "chart.js/auto";

  function formatDate(isoDate) {
    const date = new Date(isoDate);
    return date.toLocaleString();
  }

  // Function to create or update the chart
  function createOrUpdateChart() {
    const ctx = pieChart.getContext("2d");
    const colors = ["#7540BF", "#006D46", "#006D46", "#FF33E3", "#33E3FF"]; // Define colors here

    // Destroy the previous chart instance if it exists
    if (pieChart.chart) {
      pieChart.chart.destroy();
    }

    // Create a new chart
    pieChart.chart = new Chart(ctx, {
      type: "pie",
      data: {
        labels: apistuff.data.map((item) => formatDate(item.Date)), // Use names as labels
        datasets: [
          {
            data: apistuff.data.map((item) => 1), // Set all data points to 1
            backgroundColor: colors,
            borderWidth: 0, // Set borderWidth to 0 to remove the border
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
    });
  }
  // Create the initial empty chart
  onMount(() => {
    console.log(dateData);
    const ctx = pieChart.getContext("2d");
    pieChart.chart = new Chart(ctx, {
      type: "pie",
      data: {
        labels: [],
        datasets: [
          {
            data: [],
            backgroundColor: [],
          },
        ],
      },
      options: {
        responsive: true,
        maintainAspectRatio: false,
      },
    });
  });

  onMount(async () => {
    try {
      const response = await fetch(apiUrl, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ link: genlink }),
      });

      if (response.ok) {
        const data = await response.json();
        console.log(data);
        apistuff = data;

        // Extract the date data for the pie chart
        if (Array.isArray(data.data)) {
          dateData = data.data.map((item) => item.Date);

          // Call the createOrUpdateChart function when data is available
          createOrUpdateChart();
        }
      } else {
        console.error("Fetch request failed with status:", response.status);
      }
    } catch (error) {
      console.error("Error during fetch:", error);
    }
  });
</script>

<main>
  <Nav />
  <div class="container">
    <h1>Admin Info</h1>

    {#if apistuff && Array.isArray(apistuff.data) && apistuff.data.length > 0}
      <p>{apistuff.data.length} Response(s)</p>
      <a href={genlink}>Url Link </a>
    {:else}
      <p>No Responses!</p>
      <a href={genlink}>Url Link </a>
    {/if}
    <div class="pie-chart">
      <canvas bind:this={pieChart} />
    </div>
    <details>
      <summary>Detailed Info</summary>
      <table>
        <thead>
          <tr>
            <th scope="col">User</th>
            <th scope="col">Date Picked</th>
          </tr>
        </thead>
        <tbody>
          {#if apistuff && Array.isArray(apistuff.data)}
            {#each apistuff.data as item}
              <tr>
                <th scope="row">{item.Name}</th>
                <td>{formatDate(item.Date)}</td>
              </tr>
            {/each}
          {:else}
            <tr>
              <td colspan="2">No data available</td>
            </tr>
          {/if}
        </tbody>
      </table>
    </details>
  </div>
</main>

<style>
  /* Add your CSS styles for the pie chart container if needed */
  .pie-chart {
    max-width: 400px;
    margin: 1rem;

    margin-bottom: 1rem;
  }
</style>
