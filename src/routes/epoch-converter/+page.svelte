<script lang="ts">
    import BackButton from "$lib/components/BackButton.svelte";

    let source: number | null = $state(Math.floor(Date.now() / 1000));
    let resultTZ = $state("");
    let resultUTC = $state("");
    let resultRelative = $state("");
    
    function parseTimestamp() {
        if(source == null) return;
        let _ts = source;
        _ts = _ts * 1000;
        let ts = new Date(_ts);
        resultTZ = ts.toLocaleString() + " " + new Date().toString().match(/([A-Z]+[\+-][0-9]+)/)![1];
        resultUTC = ts.toUTCString();
        resultRelative = calcRelative(_ts);
    }

    function calcRelative(date: number) {
        var seconds = Math.floor((Date.now() - date) / 1000);
        var sufix = "ago";
        if(Date.now() < date) {
            var seconds = Math.floor((date - Date.now()) / 1000);
            var sufix = "in future";
        }

        var interval = seconds / 31536000;

        if (interval > 1) {
            return Math.floor(interval) + " years " + sufix;
        }
        interval = seconds / 2592000;
        if (interval > 1) {
            return Math.floor(interval) + " months " + sufix;
        }
        interval = seconds / 86400;
        if (interval > 1) {
            return Math.floor(interval) + " days " + sufix;
        }
        interval = seconds / 3600;
        if (interval > 1) {
            return Math.floor(interval) + " hours " + sufix;
        }
        interval = seconds / 60;
        if (interval > 1) {
            return Math.floor(interval) + " minutes " + sufix;
        }
        if(seconds < 5) {
            return "Just now";
        }
        return Math.floor(seconds) + " seconds " + sufix;
    }

</script>

<svelte:head>
    <title>Epoch Timestamp Converter</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
</svelte:head>

<BackButton />

<h1>Epoch Time Converter</h1>
    
<div class="main-card">
    <input id="source" bind:value="{source}" placeholder="Timestamp">
    
    <button class="btn btn-large" id="generate" onclick="{parseTimestamp}">Parse timestamp</button>

    <div class="form-box">
        <div class="form-control">
            <label for="length">Your TZ</label>
            <span>{resultTZ}</span>
        </div>
        <div class="form-control">
            <label for="uppercase">UTC</label>
            <span>{resultUTC}</span>
        </div>
        <div class="form-control">
            <label for="lowercase">Relative</label>
            <span>{resultRelative}</span>
        </div>
    </div>
</div>

<style>
#source {
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 15px;
    margin-bottom: 25px;
    position: relative;
    width: 100%;
}
.form-box {
    margin-top: 20px;
}
</style>
