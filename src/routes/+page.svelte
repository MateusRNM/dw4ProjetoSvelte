<script>
    import { goto } from '$app/navigation';
</script>

<div id="topBar">
    <center><h1>CONVERSOR DE MOEDAS</h1></center>
</div>

<div class="textBox">
    <center><p class="text">Faça conversão de moedas automaticamente. Valores sempre atualizados.</p></center>
    <button class="button" style="background-color: gold;" onclick={() => goto("./converter")}>CONVERTER</button><br>
    <button class="button" style="background-color: cyan;" onclick={() => goto("./sobre")}>SOBRE O AUTOR</button>
</div>

<style>
    * {
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    }
    h1 {
        margin-top: 1%;
    }
    #topBar {
        background-color: chartreuse;
        height: 10vh;
        width: 100%;
        position: fixed;
        top: 0px;
        border: 2px black solid;
    }
    .textBox {
        position: absolute;
        width: 50%;
        height: 40%;
        top: 50%;
        left: 50%;
        border: 5px black solid;
        transform: translate(-50%, -50%);
        padding: 1%;
        border-radius: 8px;
        box-shadow: 10px 5px 5px chartreuse;
    }
    .text { 
        font-size: 20px;
    }
    .button {
        border: none;
        box-shadow: 5px 5px 5px chartreuse;
        border-radius: 6px;
        width: 20%;
        height: 20%;
        margin-top: 2%;
        margin-left: 50%;
        transform: translateX(-50%);
    }
</style>