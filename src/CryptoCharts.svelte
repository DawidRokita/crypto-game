<script>
  import * as myjson from "./upgrades.json";
  import * as schema from "./schema.json";

  console.log(myjson);
  console.log(schema);

  let bat_rate;
  let btc_rate;
  const api_url = "https://api.zonda.exchange/rest/trading/ticker";
  async function getData() {
    const response = await fetch(api_url);
    const data = await response.json();
    console.log("rate of BAT-USD is", data["items"]["BAT-USD"]["rate"]);
    console.log(data);
    bat_rate = data["items"]["BAT-USD"]["rate"];
    btc_rate = data["items"]["BTC-USD"]["rate"];
  }

  getData();

  //zmienic svelte charts na chart.js - wiecej mozliwosci (lepszy dla tego programu)
  import {onMount} from 'svelte';
  function createChart() {
    const ctx = document.getElementById('myChart');
    const myChart = new Chart(ctx, {
      type: 'line',
      data: {
          labels: [1, 2, 3, 4, 5, 6],
          datasets: [{
              label: 'data',
              data: [12, 19, 3, 5, 2, 3],
              backgroundColor: [
                  'rgb(255,215,0)'
              ],
              borderColor: [
                  'rgb(255,215,0)'
              ],
              borderWidth: 2
          }]
      },
      options: {
          scales: {
              y: {
                  beginAtZero: true
              }
          }
      }
  });
}
onMount(createChart);

</script>

<h1>bitbay api data:</h1>
<h1>BAT: {bat_rate}</h1>
<h1>BTC: {btc_rate}</h1>
<canvas id="myChart"></canvas>

<style>
  #myChart{
    background: white;
    width: 100%;
    height: 100;
  }
</style>
