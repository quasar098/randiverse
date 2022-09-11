<script lang="ts">
    export let callback;
</script>

<div class='toolbar'>
    <h4 class='italic'>Toolbar: </h4>
    <button on:click={() => callback('clear')}>
        <p>Clear All</p>
    </button>
    <button on:click={() => callback('number')}>
        <p>Number</p>
    </button>
    <button on:click={() => callback('string')}>
        <p>String</p>
    </button>
    <button on:click={() => callback('noun')}>
        <p>Noun</p>
    </button>
    <button on:click={() => callback('adjective')}>
        <p>Adjective</p>
    </button>
    <button on:click={() => callback('verb')}>
        <p>Verb</p>
    </button>
    <button on:click={() => callback('output')} class='ml mr'>
        <i class='fa fa-rotate-right'></i>
    </button>
</div>

<style>
    .toolbar {
        height: 48px;
        width: calc(100% - 10px);
        border-top: 2px solid black;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: flex-start;
        gap: 10px;
        padding-left: 10px;
    }
    button {
        height: 30px;
    }
    button p {
        margin: 0px;
    }
    h4 {
        margin: 0px;
    }
    .ml {
        margin-left: auto;
    }
    .mr {
        margin-right: 10px;
    }
</style>
