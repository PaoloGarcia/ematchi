<script lang="ts">
	import { createEventDispatcher } from "svelte";
	import Square from "./Square.svelte";

    export let grid: string[];
    export let found: string[];

    const dispatch = createEventDispatcher();
    let firstGuess = -1;
    let secondGuess = -1;
    let clearGameTimeout: NodeJS.Timeout;

    function onClickEmoji(i: number, emoji: string): void {
        clearTimeout(clearGameTimeout);
        if (firstGuess === -1 && secondGuess === -1) {
            firstGuess = i;
        } else if (secondGuess === -1) {
            secondGuess = i;
            if (grid[firstGuess] === grid[secondGuess]) {
                // got a pair!
                dispatch("appemojifound", { emoji });
            } else {
                // incorrect, not a pair
                 clearGameTimeout = setTimeout(() => {
                    firstGuess = secondGuess = -1;
                }, 1000);
            }
        } else {
            firstGuess = i;
            secondGuess = -1;
        }
    }
</script>

<div class="grid">
    {#each grid as emoji, i}
        <Square
            {emoji}
            selected={firstGuess === i || secondGuess === i}
            found={found.includes(emoji)}
            on:click={() => onClickEmoji(i, emoji)}
        />
    {/each}
</div>

<style>
    .grid {
        display: grid;
        grid-gap: 0.5em;
        grid-template-columns: repeat(4, 1fr);
        grid-template-rows: repeat(4, 1fr);
        height: 100%;
    }
</style>