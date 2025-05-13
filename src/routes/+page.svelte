<script lang="ts">
    import Card from "./Card.svelte";
</script>

<h1>Utility Tools</h1>
    
<div class="cards-container">
    <Card title="Password Generator" href="password-generator">
        {#snippet icon()}
        <svg class="card-icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
        </svg>
        {/snippet}
        {#snippet description()}
            Generate secure, random passwords to protect your online accounts.
        {/snippet}
    </Card>

    <Card title="Base64" href="base64">
        {#snippet icon()}
        <svg class="card-icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 3v2m6-2v2M9 19v2m6-2v2M5 9H3m2 6H3m18-6h-2m2 6h-2M7 19h10a2 2 0 002-2V7a2 2 0 00-2-2H7a2 2 0 00-2 2v10a2 2 0 002 2zM9 9h6v6H9V9z" />
        </svg>
        {/snippet}
        {#snippet description()}
            Encode and decode text in Base64 for secure data transfer.
        {/snippet}
    </Card>

    <Card title="Epoch Time Converter" href="epoch-converter">
        {#snippet icon()}
        <svg class="card-icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewbox="0 0 24 24" stroke="currentcolor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
        {/snippet}
        {#snippet description()}
            Convert between Unix timestamp and human-readable date/time.
        {/snippet}
    </Card>

    <Card title="CPF Generator" href="cpf-generator">
        {#snippet icon()}
        <svg class="card-icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" d="M15 9h3.75M15 12h3.75M15 15h3.75M4.5 19.5h15a2.25 2.25 0 0 0 2.25-2.25V6.75A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25v10.5A2.25 2.25 0 0 0 4.5 19.5Zm6-10.125a1.875 1.875 0 1 1-3.75 0 1.875 1.875 0 0 1 3.75 0Zm1.294 6.336a6.721 6.721 0 0 1-3.17.789 6.721 6.721 0 0 1-3.168-.789 3.376 3.376 0 0 1 6.338 0Z" />
        </svg>
        {/snippet}
        {#snippet description()}
            Generate random and valid CPF.
        {/snippet}
    </Card>
</div>
