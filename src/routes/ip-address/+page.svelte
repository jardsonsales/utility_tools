<script lang="ts">
    import BackButton from "$lib/components/BackButton.svelte";
    import { Stretch } from 'svelte-loading-spinners';

    let result = $state("");
    let loading = $state(true);
    let copyBtnIcon = $state("far fa-clipboard");

    function copyClipboard() {
        copyBtnIcon = "fas fa-check";
        setTimeout(() => { copyBtnIcon = "far fa-clipboard" }, 1000);
        navigator.clipboard.writeText(result);
    }

    (async () => {
        const response = await fetch('https://api.ipify.org?format=json');
        const data = await response.json();
        result = data.ip;
        loading = false;
    })();
</script>

<svelte:head>
    <title>IP Address</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
</svelte:head>

<BackButton />

<h1>IP Address</h1>
    
<div class="main-card">
    <div class="result-container">
        <span id="result">{#if loading}<Stretch size="25" color="#858585" unit="px" duration="1s" />{:else}{result}{/if}</span>
        <button onclick="{copyClipboard}" class="btn btn-cpy btn-icon" id="clipboard" aria-label="Copy">
            <i class="{copyBtnIcon}"></i>
        </button>
    </div>
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
