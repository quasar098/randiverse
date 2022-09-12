<script lang="ts">
    export let data = {capitalLetters: 'first'};
</script>

<div class='chunk'>
    <p>Capitalization</p>
    <select name="cars" bind:value={data.capitalLetters}>
        <option value="none">lowercase</option>
        <option value="first">First letter</option>
        <option value="all">ALL CAPS</option>
        <option value="random">rAnDOm CapS</option>
    </select>
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
