<script lang="ts">
import { goto } from "$app/navigation";

function goHome() {
    goto("/");
}
</script>

<div class="goBackBtn" onclick="{goHome}" role="button" onkeyup="{goHome}" tabindex="0"><i class="fas fa-arrow-left"></i> Back</div>

<style>
    .goBackBtn {
        background-color: var(--card-color);
        border-radius: 12px;
        padding: 15px 20px;
        box-shadow: var(--shadow);
        position: fixed;
        left: 5px;
        top: 5px;
        color: var(--primary-color);
        cursor: pointer;
        font-weight: bold;
    }
</style>
