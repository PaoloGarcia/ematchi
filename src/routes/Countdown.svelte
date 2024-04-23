<script lang="ts">
    export let remaining: number;
    export let duration: number;
</script>

<div class="countdown">
    <button></button>
    <div class="duration">
        <div class="remaining"></div>
    </div>
</div>

<style>
    .countdown {
        display: flex;
    }

    .duration {
        flex: 1;
    }

    .remaining {
        position: absolute;
    }
</style>
