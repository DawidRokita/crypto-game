<script>
    import Timer from "./Timer.svelte";
    import Charts from "./CryptoCharts.svelte";

    //get cookies
    let cookiemoney = parseInt(document.cookie.split("x")[1]);
    let cookieaddmoney = parseInt(document.cookie.split("x")[2]);
    let cookieaddmoneyS = parseInt(document.cookie.split("x")[3]);
    let cookieup1 = parseInt(document.cookie.split("x")[4]);
    let cookieup2 = parseInt(document.cookie.split("x")[5]);

    let money = 0;
    let addmoney = 1;
    let up1 = 20;
    let up2 = 100;
    let addmoneyS = 0;
    let open = true;
    let seconds = 0;

    if (document.cookie) {
        money = cookiemoney;
        addmoney = cookieaddmoney;
        addmoneyS = cookieaddmoneyS;
        up1 = cookieup1;
        up2 = cookieup2;
    }

    function setCookie() {
        document.cookie =
            "x" +
            money +
            "x" +
            addmoney +
            "x" +
            addmoneyS +
            "x" +
            up1 +
            "x" +
            up2;
    }

    function count() {
        money += addmoney;
        setCookie();
    }
    function upgrade() {
        addmoney += 4;
        money -= up1;
        up1 += up1;
    }

    const toggle = () => open;

    function adds() {
        money += addmoneyS;
        setCookie();
    }

    function upgrade2() {
        addmoneyS += 2;
        money -= up2;
        up2 += up2;
    }
</script>

<Timer callback={adds} />

<div class="container">
    <div class="money">
        <h1>{money} coins</h1>
        <p>{addmoneyS * 2}cps | {addmoney}cpc</p>
    </div>
    <div class="clicker">
        <div class="click" on:click={count} />
    </div>
    <div class="upgradesheader">
        <!-- <h1>UPGRADES</h1> -->
    </div>
    <div class="upgrades">
        {#if money >= up1}
            <button on:click={upgrade}>kup ulepszenie +4 za {up1}</button>
        {:else}
            <button on:click={upgrade} disabled
                >kup ulepszenie +4 za {up1}</button
            >
        {/if}

        {#if money >= up2}
            <button on:click={upgrade2}>kup ulepszenie +4/s za {up2}</button>
        {:else}
            <button on:click={upgrade2} disabled
                >kup ulepszenie +4/s za {up2}</button
            >
        {/if}
    </div>
    <div class="options">
        <div class="optleft">
            <div class="opt stats">STATS</div>
            <div class="opt info">INFO</div>
        </div>
        <div class="optright">
            <div class="opt settings">OPTIONS</div>
            <div class="opt guide">GUIDE</div>
        </div>
    </div>
    <div class="tradesheader">
        <h1>TRADES</h1>
    </div>
    <div class="trades">
        <Charts />
    </div>
</div>

<style>
    .clicker {
        grid-area: a;
        /* background: #70707073; */
        display: flex;
        align-items: center;
        justify-content: center;
        /* margin: 0 25px 7rem 25px; */
    }
    .upgrades {
        grid-area: b;
        /* background: #70707073; */
        display: flex;
        align-items: center;
        justify-content: flex-start;
        flex-direction: column;
        /* margin: 10px 30px 0 0; */
        border-top-right-radius: 1rem;
    }

    .upgradesheader {
        grid-area: c;
        /* background: #70707073; */
        /* margin: 0 30px 60px 0; */
        border-bottom-right-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .options {
        grid-area: d;
        /* background: #70707073; */
        /* margin: 30px 25px 0 25px; */
        display: flex;
        align-items: center;
        justify-content: center;
        flex-wrap: wrap;
    }
    .trades {
        grid-area: e;
        /* background: #70707073; */
        /* margin: 10px 0 0 30px; */
        border-top-left-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .tradesheader {
        grid-area: f;
        /* background: #70707073; */
        /* margin: 0 0 60px 30px; */
        border-bottom-left-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .money {
        grid-area: g;
        /* background: #70707073; */
        /* margin: 0 25px 0 25px; */
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }

    .container {
        width: 100%;
        height: 100vh;
        display: grid;
        background-image: url("../img/bg.png");
        background-size: 100% 100%;
        grid-template-columns: 1fr 3fr 1fr;
        grid-template-rows: 2fr 4fr 2fr;
        grid-template-areas:
            "c g f"
            "b a e"
            "b d e";
    }
    h1 {
        font-size: xx-large;
        color: #000000;
    }
    .click {
        width: 10rem;
        height: 10rem;
        background: #353535;
        border-radius: 4rem;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .click:hover {
        background: #292929;
    }
    button {
        width: 95%;
        height: 3rem;
        margin: 10px;
        background: rgba(255, 253, 253, 0.322);
        color: none;
        border: 0;
        border-bottom: 2px solid;
        border-top-right-radius: 10px;
        border-bottom-right-radius: 10px;
        color: rgb(112, 112, 112);
    }

    button:hover {
        background: #353535;
    }

    .optleft {
        width: 50%;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }
    .optright {
        width: 50%;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        align-items: flex-end;
    }

    .opt {
        width: 80%;
        height: 4rem;
        background: #3f3f3f;
        margin: 10px;
        margin: 1rem 0 1rem 0;
    }
    p {
        color: rgb(92, 92, 92);
    }
</style>
