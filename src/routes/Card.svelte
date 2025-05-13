<script lang="ts">
    let { title, description, href, icon } = $props();
</script>

<a href="{href}" class="card">
    {@render icon()}
    <h3 class="card-title">{title}</h3>
    <p class="card-description">{@render description()}</p>
</a>
