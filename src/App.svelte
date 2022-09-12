<script lang="ts">
    import Toolbar from "./Toolbar.svelte";
    import ChunkBuilder from "./ChunkBuilder.svelte";
    import Output from "./Output.svelte";
    import { chunks, outputs, randomVerb, randomAdjective, randomNoun } from './stores.js';

    function newChunkObject(chunkName): ChunkObject {
        function chunkObjectWithoutType(): ChunkObject {
            switch (chunkName) {
                case "number":
                    return {min: 1, max: 100}
                case "string":
                    return {text: ''}
                case "noun":
                    return {capitalLetters: 'first'}
                case "adjective":
                    return {capitalLetters: 'first'}
                case "verb":
                    return {capitalLetters: 'first'}
                case "list":
                    return {possible: ""}
            }
        }
        let cObj = chunkObjectWithoutType();
        cObj.type = chunkName;
        cObj.chance = 100;
        return cObj;
    }

    function toolbarClick(chunkName) {
        switch (chunkName) {
            case "clear":
                return (() => {chunks.set([]);outputs.set([])})()
            case "output":
                return outputs.update(ops => {let curOut = getOutput(); curOut.replaceAll(" ", '').length ? ops.push(getOutput()) : undefined; return ops})
            case "clear-output":
                return outputs.set([]);
            default:
                return chunks.update(_ => {_.push(newChunkObject(chunkName)); return _})
        }
    }

    function genCapitalize(data: ChunkObject, inFunc): string {
        let text = inFunc();
        let newText = '';
        switch (data.capitalLetters) {
            case "first":
                text = text.slice(0, 1).toUpperCase() + text.slice(1);
                return text;
            case "random":
                for (let index in text) {
                    newText += (Math.random() > 0.5) ? text[index].toUpperCase() : text[index];
                }
                return newText;
            case "all":
                return text.toUpperCase();
            default:
                return text;
        }
    }

    function getOutput() {
        let text = "";
        let funcMap = new Map();
        funcMap.set("number", (data) => {
            return Math.floor(Math.random()*(data.max-data.min+1))+data.min + ""
        });
        funcMap.set("string", (data) => {
            return data.text;
        })
        funcMap.set("list", (data) => {
            let commaCount = data.possible.split(',').length-1;
            let newlineCount = data.possible.split('\n').length-1;
            let splitPossible = newlineCount >= commaCount ? data.possible.split('\n') : data.possible.split(',');
            return splitPossible[Math.floor(Math.random()*splitPossible.length)];
        })
        funcMap.set('verb', data => genCapitalize(data, randomVerb))
        funcMap.set('adjective', data => genCapitalize(data, randomAdjective))
        funcMap.set('noun', data => genCapitalize(data, randomNoun))
        chunks.update(chunkers => {
            for (let index in chunkers) {
                let chunk = chunkers[index];
                text += Math.random() > chunk.chance/100 ? "" : (funcMap.get(chunk.type) ?? (() => {""}))(chunk)
            }
            return chunkers;
        });
        return text;
    }
</script>

<main>
    <div class='header'>
        <h1 class='italic' on:click={console.log($chunks)}>Randiverse</h1>
        <h3>Advanced random generator by <a href="https://github.com/quasar098">quasar098</a></h3>
    </div>
    <ChunkBuilder/>
    <Toolbar callback={toolbarClick}/>
    <Output/>
</main>

<style>
    h1 {
        margin: 3px;
        margin-top: 7px;
    }
    h3 {
        margin: 3px;
    }
    .header {
        height: 100px;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    a:visited {
        color: #0000ee;
    }
</style>
