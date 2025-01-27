<script>
    import { request, moedas } from '$lib/awesomeAPI.js';
    import { goto } from '$app/navigation';

    let value1 = $state(null)
    let value2 = $state(null)
    let selectValue1 = $state('')
    let selectValue2 = $state('')
    let coinData = $state({})

    async function makeRequest(){
        if(selectValue1 == "" || selectValue2 == ""){
            return
        }

        coinData = await request(selectValue1)
        convert(1)
    }

    function convert(n){
        if(selectValue1 == "" || selectValue2 == ""){
            return
        }

        const convertConst = coinData.conversion_rates[selectValue2]
        
        if(n == 1){
            value2 = (value1 * convertConst).toFixed(2)
        } else {
            value1 = (value2 / convertConst).toFixed(2)
        }
    }
    
</script>

<div id="topBar">
    <center><h1>CONVERSOR DE MOEDAS</h1></center>
</div>

<div class="box">
    <div class="currencyBox">
        <div class="currency">
            <center><h2>{selectValue1}</h2></center>
            <center><input class="valueInput" type="numeric" bind:value={value1} onchange={() => convert(1)}></center>
            <div class="dropdown">
                <div class="dropdown-select">
                    <span class="select">SELECIONE UMA MOEDA</span>
                </div>

                <div class="dropdown-list">
                    {#each moedas as moeda}
                        <div class={selectValue1 == moeda.value ? "dropdown-list-item item-selected" : "dropdown-list-item"} value={moeda.value} onclick={(e) => { 
                            selectValue1 = e.target.value
                            document.getElementsByClassName('select')[0].innerHTML = moeda.nome
                            makeRequest()
                        }}>{moeda.nome}</div>
                    {/each}
                </div>
            </div>
        </div>

        <p>=</p>

        <div class="currency" style="left: 55%; top: -30%;">
            <center><h2>{selectValue2}</h2></center>
            <center><input class="valueInput" type="numeric" bind:value={value2} onchange={() => convert(2)}></center>
            <div class="dropdown">
                <div class="dropdown-select">
                    <span class="select">SELECIONE UMA MOEDA</span>
                </div>

                <div class="dropdown-list">
                    {#each moedas as moeda}
                        <div class={selectValue2 == moeda.value ? "dropdown-list-item item-selected" : "dropdown-list-item"} value={moeda.value} onclick={(e) => { 
                            selectValue2 = e.target.value
                            document.getElementsByClassName('select')[1].innerHTML = moeda.nome
                            makeRequest()
                        }}>{moeda.nome}</div>
                    {/each}
                </div>
            </div>
        </div>

        <button class="button" style="background-color: gold;" onclick={() => goto("/")}>VOLTAR AO INÍCIO</button><br>
        <button class="button" style="background-color: cyan; left: 62%; top: -0%;" onclick={() => goto("/sobre")}>SOBRE O AUTOR</button>

    </div>
</div>

<style>
    * {
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    }
    h1 {
        margin-top: 1%;
    }
    p {
        position: absolute;
        font-size: 50px;
        left: 50%;
        top: 50%;
        width: fit-content;
        height: fit-content;
        transform: translate(-50%, -50%);
    }
    .button {
        position: relative;
        left: 40%;
        top: 20%;
        border: none;
        box-shadow: 5px 5px 5px chartreuse;
        border-radius: 6px;
        width: 20%;
        height: 20%;
        transform: translateX(-50%);
    }
    #topBar {
        background-color: chartreuse;
        height: 10vh;
        width: 100%;
        position: fixed;
        top: 0px;
        border: 2px black solid;
    }
    .box {
        position: absolute;
        width: 50%;
        height: 60%;
        top: 45%;
        left: 50%;
        border: 5px black solid;
        transform: translate(-50%, -50%);
        padding: 1%;
        border-radius: 8px;
        box-shadow: 10px 5px 5px chartreuse;
    }
    .currencyBox {
        position: relative;
        width: 99%;
        height: 99%;
        padding: 1%;
    }
    .currency {
        position: relative;
        top: 20%;
        left: 5%;
        width: 40%;
        height: 50%;
        border: 3px black solid;
        padding: 1%;
        border-radius: 8px;
    }
    .valueInput {
        border: 3px black solid;
        padding: 1%;
        border-radius: 8px;
        text-align: center;
        color: black;
    }
    .dropdown {
        position: absolute;
        top: 120%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 80%;
    }
    .dropdown:hover .dropdown-list {
        opacity: 1;
        visibility: visible;
    }
    .dropdown-select {
        padding: 2%;
        border-radius: 4px;
        background-color: white;
        border: 3px black solid;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-size: 16px;
        cursor: pointer;
    }
    .dropdown-list {
        border-radius: 4px;
        border: 3px black solid;
        background-color: white;
        margin-top: 1.5%;
        opacity: 0;
        visibility: hidden;
        transition: opacity 0.2s linear, visibility 0.2s linear;
        overflow: auto;
        width: 100%;
        height: 10rem;
    }
    .dropdown-list-item {
        padding-left: 2%;
        padding-top: 2%;
        font-size: 16px;
        cursor: pointer;
        background-color: white;
        border-radius: 4px;
        transition: background-color 0.3s linear;
    }
    .dropdown-list-item:hover {
        padding-left: 4%;
        background-color: chartreuse;
    }
    .select {
        text-align: center;
    }
    .item-selected {
        background-color: gold;
    }
</style>