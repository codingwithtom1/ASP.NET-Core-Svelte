<script>
    function getForecasts() {
    return fetch('/weatherforecast')
      .then(response => response.json())

  }
  </script>
  
  <style>
    /* add some styling for the table */
    table {
      border-collapse: collapse;
      width: 100%;
    }
  
    th, td {
      border: 1px solid black;
      padding: 10px;
      text-align: left;
    }
  </style>
  
<h1>Weather Forecasts</h1>
  {#await getForecasts()}
  <h2>Loading...</h2>
  {:then weatherData}
  <table>
    <thead>
      <tr>
        <th>Date</th>
        <th>Temperature (°C)</th>
        <th>Temperature (°F)</th>
        <th>Summary</th>
      </tr>
    </thead>
    <tbody>

  {#each weatherData as { date, temperatureC, temperatureF, summary }}

  <tr>
    <td>{date}</td>
    <td>{temperatureC}</td>
    <td>{temperatureF}</td>
    <td>{summary}</td>
  </tr>
   
  {/each}
</tbody>
</table>

{/await}
