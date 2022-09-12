<script lang="ts">
    export let data;
    export let isfirst = false;
    export let islast = false;
    import Number from './chunks/Number.svelte'
    import String from './chunks/String.svelte'
    import Noun from './chunks/Noun.svelte';
    import Verb from './chunks/Verb.svelte';
    import Adjective from './chunks/Adjective.svelte';
    import List from './chunks/List.svelte';
    import { chunks } from './stores.js'

    function determineColor(): string {
        switch (data.type) {
            case "number":
                return "186, 215, 242";
            case "string":
                return "143, 247, 167";
            case "noun":
                return "242, 186, 201";
            case "verb":
                return "242, 226, 186";
            case "adjective":
                return "242, 206, 230";
            default:
                return "229, 229, 229";
        }
    }
    function moveLeft() {
        chunks.update(chunkers => {
            let index = chunkers.indexOf(data)
            chunkers = chunkers.filter(chunky => chunky != data);
            chunkers.splice(index-1, 0, data);
            return chunkers;
        })
    }
    function moveRight() {
        chunks.update(chunkers => {
            let index = chunkers.indexOf(data)
            chunkers = chunkers.filter(chunky => chunky != data);
            chunkers.splice(index+1, 0, data);
            return chunkers;
        })
    }
</script>

<div class='chunk-outer' style="background-color: rgb({determineColor()})">
    <h2>{data.type}</h2>
    <i class='fa fa-file' title="duplicate" on:click={chunks.update((chunkers) => {chunkers.push({...data}); return chunkers})}></i>
    <i class='fa fa-close' title="delete" on:click={chunks.set($chunks.filter(chunk => chunk != data))}></i>
    <i class='fa fa-arrow-left' title="move left" on:click={moveLeft} style="display: {isfirst ? 'none' : 'block'}"></i>
    <i class='fa fa-arrow-right' title="move right" on:click={moveRight} style="display: {islast ? 'none' : 'block'}"></i>
    <div class='chunk-middle'>
        {#if data.type == "number"}
            <Number bind:data={data}/>
        {:else if data.type == "string"}
            <String bind:data={data}/>
        {:else if data.type == "noun"}
            <Noun bind:data={data}/>
        {:else if data.type == "adjective"}
            <Adjective bind:data={data}/>
        {:else if data.type == "verb"}
            <Verb bind:data={data}/>
        {:else if data.type == "list"}
            <List bind:data={data}/>
        {/if}
    </div>
</div>

<style>
    .fa {
        font-size: 20px;
        position: absolute;
        background-color: #88888888;
        width: 22px;
        height: 22px;
        text-align: center;
        border-radius: 3px;
        z-index: 10;
    }
    .fa-close {
        top: 10px;
        right: 10px;
    }
    .fa-file {
        top: 10px;
        left: 10px;
    }
    .fa-arrow-left {
        top: 37px;
        left: 10px;
    }
    .fa-arrow-right {
        top: 37px;
        right: 10px;
    }
    .chunk-outer {
        border-right: 1px rgb(79, 79, 79) outset;
        border-left: 1px rgb(79, 79, 79) outset;
        height: 298px;
        width: 200px;
        display: inline-flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        position: relative;
    }
    .chunk-middle {
        flex-direction: row;
        justify-content: flex-start;
        align-items: center;
    }
</style>
