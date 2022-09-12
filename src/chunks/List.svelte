<script lang="ts">
    export let data = {possible: '', chance: 100};
</script>

<div class='chunk'>
    <p>Possible strings</p>
    <textarea bind:value={data.possible}></textarea>
    <p>Chance to show up</p>
    <input type="value" bind:value={data.chance} step="1"/>
</div>

<style>
    textarea {
        width: 165px;
        height: 100px;
        resize: none;
    }
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
