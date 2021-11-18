<script>
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
</script>

<h1>bitbay api data:</h1>
<h1>{bat_rate}</h1>
<h1>{btc_rate}</h1>