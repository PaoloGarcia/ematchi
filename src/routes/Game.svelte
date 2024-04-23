<script lang="ts">
	import Countdown from "./Countdown.svelte";
    import Grid from "./Grid.svelte";
	import Found from "./Found.svelte";
	import { levels, type Level } from "./levels";
	import { shuffle } from "./utils";

    const level: Level = levels[0];
    let size: number = level.size;
    let grid: string[] = createGrid(level);
    let found: string[] = [];

    function createGrid(level: Level): string[] {
        const copy = level.emojis.slice();
        const pairs: string[] = [];
        for (let i = 0; i < size ** 2 / 2; i++) {
            const index = Math.floor(Math.random() * size);
            const emoji = copy[index]

            copy.splice(index, 1);
            pairs.push(emoji);
        }
        pairs.push(...pairs);
        return shuffle(pairs);
    }

    function onFoundEmoji(event: CustomEvent): void {
        found = [...found, event.detail.emoji];
    }
</script>

<main class="game">
    <section class="info">
        <Countdown remaining={level.duration} duration={level.duration} />
    </section>
    <section class="grid-container">
        <Grid {grid} on:appemojifound={onFoundEmoji} {found} />
    </section>
    <section class="info">
        <Found {found} />
    </section>
</main>

<style>
    .game {
        align-items: center;
        display: flex;
        flex-direction: column;
        font-size: min(1vmin, 0.3rem);
        justify-content: center;
    }

    .info {
        background-color: purple;
        height: 10em;
        width: 80em;
    }

    .grid-container {
        background-color: teal;
        height: 80em;
        width: 80em;
    }
</style>
