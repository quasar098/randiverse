<script lang="ts">
    export let data = {text: '', chance: 100};
</script>

<div class='chunk'>
    <p>Text</p>
    <input type="text" bind:value={data.text} step="1"/>
    <p>Chance to show up</p>
    <input type="value" bind:value={data.chance} step="1"/>
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
    }
</style>
