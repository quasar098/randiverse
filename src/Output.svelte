<script lang="ts">
    import { outputs } from './stores.js';


</script>

<div class='output'>
    {#each [...$outputs].reverse() as output}
        <p>{output}</p>
    {/each}
</div>

<style>
    .output {
        position: absolute;
        bottom: 0px;
        top: 450px;
        width: 100%;
        border-top: 2px solid black;
        background-color: #dddddd;
        overflow-y: auto;
    }
    p {
        margin: 3px;
    }
</style>
