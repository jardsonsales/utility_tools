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

    function randomNumber(): string { 
        return ("" + Math.floor(Math.random() * 999)).padStart(3, '0'); 
    }

    function dig(n1: string, n2: string, n3: string, n4?: string): number { 
        let nums = n1.split("").concat(n2.split(""), n3.split(""), n4 ? [n4] : []), x = 0;  
        for (let i = (n4 !== undefined ? 11 : 10), j = 0; i >= 2; i--, j++) { 
            x += +nums[j] * i; 
        } 
        let y = x % 11; 
        return y < 2 ? 0 : 11 - y; 
    }

    function generateCpf(): void { 
        const n1 = randomNumber(), n2 = randomNumber(), n3 = randomNumber(), d1 = dig(n1, n2, n3).toString(); 
        const cpf = `${n1}.${n2}.${n3}-${d1}${dig(n1, n2, n3, d1.toString())}`;
        result = (mask == "0" ? cpf.replaceAll(/[^0-9]/g, "") : cpf); 
    }

    onMount(() => {
        generateCpf();
    });
</script>

<svelte:head>
    <title>CPF Generator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
</svelte:head>

<BackButton />

<h1>CPF Generator</h1>
    
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

    <button class="btn btn-large" id="generate" onclick="{generateCpf}">Generate CPF</button>
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
