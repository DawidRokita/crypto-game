<script>
    import Timer from "./Timer.svelte";
    import Charts from "./CryptoCharts.svelte";
    import Stats from "../files/stats.svelte";
    import Info from "../files/info.svelte";
    import Settings from "../files/settings.svelte";
    import Guide from "../files/guide.svelte";
    // import { set_style } from "svelte/internal";

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

    function optClick(option) {
        const stats = document.querySelector(".statsOpt");
        const info = document.querySelector(".infoOpt");
        const setting = document.querySelector(".settingOpt");
        const guide = document.querySelector(".guideOpt");
        console.log({ option });
        switch (option) {
            case "stats":
                stats.style.display = "block";
                info.style.display = "none";
                setting.style.display = "none";
                guide.style.display = "none";
                break;
            case "info":
                stats.style.display = "none";
                info.style.display = "block";
                setting.style.display = "none";
                guide.style.display = "none";
                break;
            case "options":
                stats.style.display = "none";
                info.style.display = "none";
                setting.style.display = "block";
                guide.style.display = "none";
                break;
            case "guide":
                stats.style.display = "none";
                info.style.display = "none";
                setting.style.display = "none";
                guide.style.display = "block";
                break;
            default:
        }
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
    <div class="upgradesheader" />
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
            <div
                class="opt stats"
                on:click={() => {
                    optClick("stats");
                }}
            >
                STATS
            </div>
            <div
                class="opt info"
                on:click={() => {
                    optClick("info");
                }}
            >
                INFO
            </div>
            <div
                class="opt settings"
                on:click={() => {
                    optClick("options");
                }}
            >
                OPTIONS
            </div>
            <div
                class="opt guide"
                on:click={() => {
                    optClick("guide");
                }}
            >
                GUIDE
            </div>
        </div>
        <div class="subopt">
            <div class="statsOpt"><Stats /></div>
            <div class="infoOpt"><Info /></div>
            <div class="settingOpt"><Settings /></div>
            <div class="guideOpt"><Guide /></div>
        </div>
    </div>
    <div class="tradesheader" />
    <div class="trades">
        <Charts />
    </div>
</div>

<style>
    .clicker {
        grid-area: a;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .upgrades {
        grid-area: b;
        display: flex;
        align-items: flex-start;
        justify-content: flex-start;
        flex-direction: column;
        border-top-right-radius: 1rem;
    }
    .upgradesheader {
        grid-area: c;
        border-bottom-right-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .options {
        grid-area: d;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        flex-direction: column;
    }
    .trades {
        grid-area: e;
        border-top-left-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .tradesheader {
        grid-area: f;
        border-bottom-left-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    .money {
        grid-area: g;
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
        grid-template-rows: 2fr 4fr 2.2fr;
        grid-template-areas:
            "c g f"
            "b a e"
            "b d e";
    }
    h1 {
        font-size: xx-large;
        color: #ffd700;
    }
    .click {
        width: 15rem;
        height: 15rem;
        background-image: url("../img/click.png");
        background-size: 100% 100%;
        border-radius: 4rem;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .click:hover {
        width: 17rem;
        height: 17rem;
    }
    button {
        width: 85%;
        height: 3rem;
        margin-top: 30px;
        background: #855e42;
        color: none;
        border: 0;
        border-bottom: 2px solid;
        border-top-right-radius: 5px;
        border-bottom-right-radius: 5px;
        color: #ffffff;
    }
    button:hover {
        background: #6b4b34;
    }
    .optleft {
        width: 90%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
    }
    .subopt {
        width: 90%;
        height: 100%;
    }
    .opt {
        width: 25%;
        height: 2.5rem;
        background: #855e42;
        margin: 10px 2px 0 2px;
        border-radius: 5px;
        text-align: center;
    }
    .opt:hover {
        background: #6b4b34;
    }
    p {
        color: #ffd9009d;
    }
    .statsOpt,
    .infoOpt,
    .settingOpt,
    .guideOpt {
        width: 100%;
        height: 100%;
        /* background: rgba(255, 255, 255, 0.411); */
        display: none;
    }
</style>
