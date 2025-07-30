<script lang="ts">
    import BackButton from "$lib/components/BackButton.svelte";

    let source = $state("");
    let result = $state("");

    function selectTextarea(event: any) {
        event.target.select();
    }

    function encode() {
        result = btoa(source);
    }

    function decode() {
        result = atob(source);
    }
</script>

<svelte:head>
    <title>Base 64</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
</svelte:head>

<BackButton />

<h1>Base 64</h1>
    
<div class="main-card">
    <div class="">
        <textarea bind:value={source} onclick="{selectTextarea}"></textarea>
    </div>

    <div class="flex-buttons">
        <button class="btn" id="generate" onclick="{encode}">Encode</button>
        <button class="btn" id="generate" onclick="{decode}">Decode</button>
    </div>

    <div class="result-box">
        <textarea bind:value={result} onclick="{selectTextarea}" readonly></textarea>
    </div>
</div>

<style>
textarea {
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 15px;
    margin-bottom: 25px;
    position: relative;
    width: 100%;
    height: 80px;
}
.result-box {
    margin-top: 20px;
    margin-bottom: 0px;
}
.flex-buttons {
    display: flex;
    justify-content: space-around;
}
.flex-buttons .btn {
    font-size: 1.2rem;
}
.result-box textarea {
    background-color: rgba(0, 0, 0, 0.05);
    margin-bottom: 0px;
}

</style>
