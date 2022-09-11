<script lang="ts">
    import { chunks } from './stores.js';
    import ChunkRouter from './ChunkRouter.svelte'
</script>

<div class='chunk-builder'>
    {#each $chunks as chunk}
        <ChunkRouter bind:data={chunk}/>
    {/each}
</div>

<style>
    .chunk-builder {
        height: 298px;
        width: 100%;
        border-top: 2px solid black;
        overflow-y: hidden;
        white-space: nowrap;
    }
</style>
