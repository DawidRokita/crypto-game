<script>
    import * as myjson from './upgrades.json';
    import * as schema from './schema.json';
  
   console.log(myjson);
   console.log(schema);

  //   let bat_rate;
  //   let btc_rate;
  //   const api_url = "https://api.zonda.exchange/rest/trading/ticker";
  //   async function getData() {
  //       const response = await fetch(api_url);
  //       const data = await response.json();
  //       console.log("rate of BAT-USD is", data["items"]["BAT-USD"]["rate"]);
  //       console.log(data);
  //       bat_rate = data["items"]["BAT-USD"]["rate"];
  //       btc_rate = data["items"]["BTC-USD"]["rate"];
  //   }

  //   getData();
  import FusionCharts from 'fusioncharts';
  import Timeseries from 'fusioncharts/fusioncharts.timeseries';
  import SvelteFC, { fcRoot } from 'svelte-fusioncharts';

  fcRoot(FusionCharts, Timeseries);

  let promise,
    jsonify = res => res.json(),
    dataFetch = fetch(
      // 'https://s3.eu-central-1.amazonaws.com/fusion.store/ft/data/candlestick-chart-data.json'
      myjson
    ).then(jsonify),
    schemaFetch = fetch(
      // 'https://s3.eu-central-1.amazonaws.com/fusion.store/ft/schema/candlestick-chart-schema.json'
      schema
    ).then(jsonify);

  promise = Promise.all([dataFetch, schemaFetch]);
  
  const getChartConfig = ([data, schema]) => {
    const fusionDataStore = new FusionCharts.DataStore(),
      fusionTable = fusionDataStore.createDataTable(data, schema);

    return {
      type: 'timeseries',
      width: '100%',
      height: 450,
      renderAt: 'chart-container',
      dataSource: {
        data: fusionTable,
        caption: {
          text: "Apple Inc. Stock Price"
        },
        subcaption: {
          text: "Stock prices from January 1980 - November 2011"
        },
        yaxis: [
          {
            plot: {
              value: {
                open: "Open",
                high: "High",
                low: "Low",
                close: "Close"
              },
              type: "candlestick"
            },
            format: {
              prefix: "$"
            },
            title: "Stock Value"
          }
        ]
      }
    };
  };
</script>

<!-- <h1>bitbay api data:</h1>
<h1>BAT: {bat_rate}</h1>
<h1>BTC: {btc_rate}</h1> -->
<div id="chart-container" >
  {#await promise}
    <p>Fetching data and schema...</p>
  {:then value}
    <SvelteFC
      {...getChartConfig(value)}
    />
  {:catch error}
    <p>Something went wrong: {error.message}</p>
  {/await}
</div>