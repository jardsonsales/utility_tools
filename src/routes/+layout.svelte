<script lang="ts">
    let { children } = $props();
    import '$lib/styles/Main.css';
    import Footer from './Footer.svelte';
</script>

{@render children()}

<Footer />
