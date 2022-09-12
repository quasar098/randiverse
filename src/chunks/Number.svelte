<script lang="ts">
    export let data = {min: 1, max: 100};
</script>

<div class='chunk'>
    <p>Minimum</p>
    <input type="number" bind:value={data.min} step="1"/>
    <p>Maximum</p>
    <input type="number" bind:value={data.max} step="1"/>
    <p>Both min and max are <br><strong>inclusive</strong></p>
</div>

<style>
    .chunk {
        width: 200px;
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
    }
    p {
        text-align: center;
        margin-top: 4px;
        margin-bottom: 3px;
    }
</style>
