<script lang="ts">
    export let data = {text: ''};
</script>

<div class='chunk'>
    <p>Text</p>
    <input type="text" bind:value={data.text} step="1"/>
    <p>This is <strong>not</strong> randomized</p>
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
