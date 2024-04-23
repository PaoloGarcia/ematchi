<script lang="ts">
    export let found: string[];
</script>

<div class="found">
    {#each found as emoji (emoji)}
        <span>{emoji}</span>
    {/each}
</div>

<style>
    .found {
        align-items: center;
        display: flex;
        gap: 0.5em;
        height: 100%;
        justify-content: center;
    }

    span {
        font-size: 5em;
    }
</style>