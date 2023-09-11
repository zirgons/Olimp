<script>
	import { slide } from 'svelte/transition';
    import { fly } from 'svelte/transition';

	export let olimpiadesData = {"title": "title", "inside": "inside"};
    let open = false;
</script>

<style lang="scss">
    .block{
        height: 100px;
        width: 100%;
        text-align: center;
        background-color: gray;
        display: flex ;
        flex-direction: column;
        border-style: solid;
        border-color: black;
        border-radius: 15px;
        border-width: 2px;
        transition: 0.3s;
        margin-top: 10px;
    }
    .inside{
        box-sizing: border-box;
        width: 98%;
        margin: auto;
        text-align: center;
        background-color: gainsboro; 
        padding: 10px;
        white-space: pre-line;

        border-style: solid;
        border-color: rgb(110, 110, 110);
        border-radius: 0px 0px 10px 10px;
        border-width: 0px 2px 2px 2px;
    }
</style>



<button class="block" on:click={() => open=!open}>
    <p>{olimpiadesData.title}</p>
</button>
<div>
{#if open}
<div class="inside" transition:slide={{duration:200, delay:100, axis:'y'}}>
    <p in:fly={{duration:400, delay:200, x:-500}}>{olimpiadesData.inside}</p>
</div>
{/if}
</div>