<script lang="ts">
    export let emoji: string;
    export let selected: boolean;
    export let found: Boolean;
</script>

<div class="square" class:flipped={selected}>
    <button on:click></button>
    {#if !found}
        <span>{emoji}</span>
    {/if}
</div>

<style>
    .square {
        align-items: center;
        background-color: yellow;
        display: flex;
        justify-content: center
    }

    .flipped button {
        background-color: red;
    }

    button {
        height: 100%;
        position: absolute;
        width: 100%;
    }

    span {
        font-size: 9em;
        pointer-events: none;
    }
</style>
