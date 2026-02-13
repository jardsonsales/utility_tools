<script lang="ts">
    import { onMount } from "svelte";
    import BackButton from "$lib/components/BackButton.svelte";

    let result = $state("");
    let length = $state(25);
    let uppercase = $state(true);
    let lowercase = $state(true);
    let onlyatof = $state(false);
    let numbers = $state(true);
    let symbols = $state(false);
    let copyBtnIcon = $state("far fa-clipboard");

    function copyClipboard() {
        copyBtnIcon = "fas fa-check";
        setTimeout(() => { copyBtnIcon = "far fa-clipboard" }, 1000);
        navigator.clipboard.writeText(result);
    }

    function generatePassword() {
        if(length < 6) length = 6;
        var charset = "";
        if(lowercase) charset += (onlyatof ? "abcdefabcdefabcdef" : "abcdefghijklmnopqrstuvwxyz");
        if(uppercase) charset += (onlyatof ? "ABCDEFABCDEFABCDEF" : "ABCDEFGHIJKLMNOPQRSTUVWXYZ");
        if(numbers) charset += "0123456789012345678901234567890123456789";
        if(symbols) charset += "%#!@_-())%#!@_%#!-)(";

        var retVal = "";
        for (var i = 0, n = charset.length; i < length; ++i) {
            retVal += charset.charAt(Math.floor(Math.random() * n));
        }

        if(lowercase && retVal.match(/[a-z]/g) == null) return generatePassword();
        if(uppercase && retVal.match(/[A-Z]/g) == null) return generatePassword();
        if(numbers && retVal.match(/[0-9]/g) == null) return generatePassword();
        if(symbols && retVal.match(/[%#!@_\-()\$]/g) == null) return generatePassword();

        result = retVal;
    }

    onMount(() => {
        generatePassword();
    });
</script>

<svelte:head>
    <title>Password Generator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
</svelte:head>

<BackButton />

<h1>Password Generator</h1>
    
<div class="main-card">
    <h2>Generate Secure Password</h2>
    
    <div class="result-container">
        <span id="result">{result}</span>
        <button onclick="{copyClipboard}" class="btn btn-cpy btn-icon" id="clipboard" aria-label="Copy">
            <i class="{copyBtnIcon}"></i>
        </button>
    </div>
    
    <div class="form-box">
        <div class="form-control">
            <label for="length">Password Length</label>
            <input bind:value="{length}" type="number" id="length" min="6" max="60">
        </div>
        <div class="form-control">
            <label for="uppercase">Include uppercase letters</label>
            <input bind:checked="{uppercase}" type="checkbox" id="uppercase">
        </div>
        <div class="form-control">
            <label for="lowercase">Include lowercase letters</label>
            <input bind:checked="{lowercase}" type="checkbox" id="lowercase">
        </div>
        <div class="form-control">
            <label for="numbers">Include numbers</label>
            <input bind:checked="{numbers}" type="checkbox" id="numbers">
        </div>
        <div class="form-control">
            <label for="symbols">Include symbols</label>
            <input bind:checked="{symbols}" type="checkbox" id="symbols">
        </div>
        <div class="form-control">
            <label for="onlyatof">Only A to F letters</label>
            <input bind:checked="{onlyatof}" type="checkbox" id="onlyatof">
        </div>
    </div>
    
    <button class="btn btn-large" id="generate" onclick="{generatePassword}">Generate Password</button>
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
