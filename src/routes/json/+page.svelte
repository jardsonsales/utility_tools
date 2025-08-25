<script lang="ts">
    import BackButton from "$lib/components/BackButton.svelte";
    import { JSONEditor, Mode } from 'svelte-jsoneditor'
    import { onMount } from 'svelte';

    let mode: Mode = Mode.text; // ou Mode.text / Mode.tree
    let editorRef: JSONEditor

    onMount(() => {
        document.documentElement.style.setProperty("--jse-font-size-mono", "1.2rem");
        document.documentElement.style.setProperty("--jse-theme-color", "#4361ee");
    });

</script>

<svelte:head>
    <title>JSON Editor</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css">
</svelte:head>

<BackButton />

<h1>JSON Editor</h1>
    
<div class="main-card">
    <div>
      <JSONEditor bind:this={editorRef} {mode} indentation="    "  />
    </div>
</div>

<style>
.main-card {
    max-width: 1000px;
    min-height: 500px;
}
:global(.jse-main) {
    height: 500px !important;
}
</style>
