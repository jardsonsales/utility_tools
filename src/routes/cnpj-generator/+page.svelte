<script lang="ts">
    import { onMount } from "svelte";
    import BackButton from "$lib/components/BackButton.svelte";

    let result = $state("");
    let mask = $state("1");
    let copyBtnIcon = $state("far fa-clipboard");

    function copyClipboard() {
        copyBtnIcon = "fas fa-check";
        setTimeout(() => { copyBtnIcon = "far fa-clipboard" }, 1000);
        navigator.clipboard.writeText(result);
    }

    function generateCNPJ(): void {
        const randomDigits: number[] = [];
        for (let i = 0; i < 8; i++) {
            randomDigits.push(Math.floor(Math.random() * 10));
        }

        const allTwelveDigits = [...randomDigits, 0, 0, 0, 1];

        const weights1 = [5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
        let sum1 = 0;
        for (let i = 0; i < 12; i++) {
            sum1 += allTwelveDigits[i] * weights1[i];
        }
        const remainder1 = sum1 % 11;
        const digit1 = remainder1 < 2 ? 0 : 11 - remainder1;

        const weights2 = [6, 5, 4, 3, 2, 9, 8, 7, 6, 5, 4, 3, 2];
        const allDigits = [...allTwelveDigits, digit1];
        let sum2 = 0;
        for (let i = 0; i < 13; i++) {
            sum2 += allDigits[i] * weights2[i];
        }
        const remainder2 = sum2 % 11;
        const digit2 = remainder2 < 2 ? 0 : 11 - remainder2;

        const fullCNPJ = [...allTwelveDigits, digit1, digit2];
        const cnpjString = fullCNPJ.join('');
        result = (mask == "0" ? cnpjString : `${cnpjString.slice(0, 2)}.${cnpjString.slice(2, 5)}.${cnpjString.slice(5, 8)}/${cnpjString.slice(8, 12)}-${cnpjString.slice(12, 14)}`)
    }

    onMount(() => {
        generateCNPJ();
    });
</script>

<svelte:head>
    <title>CNPJ Generator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
</svelte:head>

<BackButton />

<h1>CNPJ Generator</h1>
    
<div class="main-card">
    <div class="result-container">
        <span id="result">{result}</span>
        <button onclick="{copyClipboard}" class="btn btn-cpy btn-icon" id="clipboard" aria-label="Copy">
            <i class="{copyBtnIcon}"></i>
        </button>
    </div>


    <div class="form-control">
        <label for="numbers">Masked result</label>
        <div class="flex">Yes <input bind:group="{mask}" type="radio" name="mask" value="1" /> No <input bind:group="{mask}" type="radio" name="mask" value="0" /></div>
    </div>

    <button class="btn btn-large" id="generate" onclick="{generateCNPJ}">Generate CNPJ</button>
</div>

<style>
.result-container {
    background-color: rgba(0, 0, 0, 0.05);
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 15px;
    margin-bottom: 25px;
    position: relative;
}
#result {
    word-wrap: break-word;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    max-width: calc(100% - 40px);
    font-family: 'Courier New', monospace;
}
</style>
