<script>
	import { slide } from 'svelte/transition';
    import { fly } from 'svelte/transition';

	export let olimpiadesData = {"title": "title", "inside": "inside"};
    let open = false;
</script>

<style lang="scss">
    
    @mixin start{
        text-align: center;
    }
    .block{
        &:hover{
            background-color: #979797;
        }
        @include start;    
        width: 100%;
        background-color: #a1a1a1;
        display: flex;
        flex-direction: column;
        border-style: solid;
        border-color: black;
        border-radius: 10px;
        border-width: 2px;
        transition: 0.3s;
        margin-top: 10px;
        padding: 10px;
    }
    .inside{
        @include start;
        overflow: hidden;
        display: flex;
        box-sizing: border-box;
        width: 98%;
        margin: auto;
        background-color: gainsboro; 
        padding: 10px;
        white-space: pre-line;

        border-style: solid;
        border-color: rgb(110, 110, 110);
        border-radius: 0px 0px 10px 10px;
        border-width: 0px 2px 2px 2px;
        justify-content: space-evenly;
    }
</style>



<button class="block" on:click={() => open=!open}>
    <h2>{olimpiadesData.title}</h2>
</button>
<div>
{#if open}
<div class="inside" transition:slide={{duration:300, delay:100, axis:'y'}}>
    <p in:fly={{duration:200, delay:350, x:-500}} out:fly={{duration:400, delay:0, x:-500}}>{olimpiadesData.inside}</p>
    <p in:fly={{duration:200, delay:300, x:-500}} out:fly={{duration:400, delay:50, x:-500}}>{olimpiadesData.inside}</p>
    <p in:fly={{duration:200, delay:250, x:-500}} out:fly={{duration:400, delay:100, x:-500}}>{olimpiadesData.inside}</p>
    <p in:fly={{duration:200, delay:200, x:-500}} out:fly={{duration:400, delay:150, x:-500}}>{olimpiadesData.inside}</p>
</div>
{/if}
</div>