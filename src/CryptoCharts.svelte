<script>
    let bat_rate;
    const api_url = "https://api.zonda.exchange/rest/trading/ticker";
    async function getData() {
        const response = await fetch(api_url);
        const data = await response.json();
        console.log("rate of BAT-USD is", data["items"]["BAT-USD"]["rate"]);
        console.log(data);
        bat_rate = data["items"]["BAT-USD"]["rate"];
    }

    getData();
</script>

<h1>{bat_rate}</h1>