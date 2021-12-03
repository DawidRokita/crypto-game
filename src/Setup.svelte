<script>
    import Timer from "./Timer.svelte";
    import Charts from "./CryptoCharts.svelte";
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

    function optClick(option){
        const opt = document.querySelector('.optleft');
        const opt2 = document.querySelector('.optright');
        const back = document.querySelector('.back');
        const stats = document.querySelector('.statsOpt');
        const info = document.querySelector('.infoOpt');
        const setting = document.querySelector('.settingOpt');
        const guide = document.querySelector('.guideOpt');
        opt.style.display = "none";
        opt2.style.display = "none";
        back.style.display = "block";
        console.log({option});
        switch(option){
            case 'stats': stats.style.display="block"; break;
            case 'info': info.style.display="block"; break;
            case 'options': setting.style.display="block"; break;
            case 'guide': guide.style.display="block"; break;
            default: ;
        }
    }

    function goBack(){
        const opt = document.querySelector('.optleft');
        const opt2 = document.querySelector('.optright');
        const back = document.querySelector('.back');
        const stats = document.querySelector('.statsOpt');
        const info = document.querySelector('.infoOpt');
        const setting = document.querySelector('.settingOpt');
        const guide = document.querySelector('.guideOpt');
        opt.style.display = "flex";
        opt2.style.display = "flex";
        back.style.display = "none";
        stats.style.display = "none";
        info.style.display = "none";
        setting.style.display = "none";
        guide.style.display = "none";
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
        <div class="statsOpt">stats</div>
        <div class="infoOpt">info</div>
        <div class="settingOpt">settings</div>
        <div class="guideOpt">guide</div>
        <div class="optleft">
            <div class="opt stats" on:click={()=>{optClick('stats');}}>STATS</div>
            <div class="opt info" on:click={()=>{optClick('info');}}>INFO</div>
        </div>
        <div class="optright">
            <div class="opt settings" on:click={()=>{optClick('options');}}>OPTIONS</div>
            <div class="opt guide" on:click={()=>{optClick('guide');}}>GUIDE</div>
        </div>
        <div class="back" on:click={goBack}>back</div>
    </div>
    <div class="tradesheader">
        <!-- <h1>TRADES</h1> -->
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
        align-items: flex-start;
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
        flex-direction: row;
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
        color: #ffd700;
    }
    .click {
        width: 10rem;
        height: 10rem;
        background: #ffd700;
        border-radius: 4rem;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .click:hover {
        background: #292929;
    }
    button {
        width: 85%;
        height: 3rem;
        margin-top: 30px;
        background: #ffd9009d;
        color: none;
        border: 0;
        border-bottom: 2px solid;
        border-top-right-radius: 5px;
        border-bottom-right-radius: 5px;
        color: #ffffff;
    }

    button:hover {
        background: #99820088;
    }

    .optleft {
        width: 50%;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin-left: 2.5rem;
    }
    .optright {
        width: 50%;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        align-items: flex-end;
        margin-right: 2.5rem;
    }

    .opt {
        width: 75%;
        height: 3.5rem;
        background: #ffd9009d;
        margin: 10px;
        /* margin: 1rem 0 1rem 0; */
        border-radius: 5px;
        text-align: center;
    }
    .opt:hover{
        background: #ffd900;
    }
    p {
        color: #ffd9009d;
    }
    .back{
        display: none;
        background: white;
        width: 5rem;
        height: 3rem;
    }

    .statsOpt, .infoOpt, .settingOpt, .guideOpt{
        width: 40rem;
        height: 8rem;
        background: yellow;
        display:none;
    } 
</style>
