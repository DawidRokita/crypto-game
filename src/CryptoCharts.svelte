<script>
  import * as myjson from "./test.json";
  console.log(myjson.default["1"]["time"]);

  let bat_rate;
  let btc_rate;
  const api_url = "https://api.zonda.exchange/rest/trading/ticker";
  async function getData() {
    const response = await fetch(api_url);
    const data = await response.json();
    bat_rate = data["items"]["BAT-USD"]["rate"];
    btc_rate = data["items"]["BTC-USD"]["rate"];
  }

  getData();

  const xlabels = []; //x data chart
  const ratedata = []; //y data charts

  let arr = Object.entries(myjson.default); //json data to array
  for (let i = 0; i < arr.length; i++) {
    xlabels[i] = arr[i][1].time;
    ratedata[i] = arr[i][1].rate;
  }

  import { onMount } from "svelte";
  async function createChart() {
    await getData();
    const ctx = document.getElementById("myChart");

    const myChart = new Chart(ctx, {
      type: "line",
      data: {
        labels: xlabels,
        datasets: [
          {
            label: "data",
            data: ratedata,
            backgroundColor: "rgb(255,215,0)",
            borderColor: "rgb(255,215,0)",
            borderWidth: 2,
            pointRadius: 0,  
          },
        ],
      },
    });
  }
  async function createChart2() {
    await getData();
    const ctx = document.getElementById("myChart2");

    const myChart2 = new Chart(ctx, {
      type: "line",
      data: {
        labels: xlabels,
        datasets: [
          {
            label: "data",
            data: ratedata,
            backgroundColor: "#FFD700",
            borderColor: "#FFD700",
            borderWidth: 2,
            pointRadius: 0,
          },
        ],
      },
    });
  }
  onMount(createChart);
  onMount(createChart2);
</script>

<h1>bitbay api data:</h1>
<h1>BAT: {bat_rate}</h1>
<h1>BTC: {btc_rate}</h1>
<canvas id="myChart" />
<canvas id="myChart2" />

<style>
  #myChart {
    background: #36261B;
    width: 75%;
    margin-top: 1rem;
  }
  #myChart2 {
    background: #36261B;
    width: 75%;
    margin-top: 1rem;
  }
  h1 {
    color: white;
  }
</style>
