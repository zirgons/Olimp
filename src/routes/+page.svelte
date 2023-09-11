<script>
    import { slide } from 'svelte/transition';
    import { fly } from 'svelte/transition';

    let data = [{title: "yup yup", inside: "nopeee\ndasdadasad\nasdasdasd", money:false, open:false},
    {title: "Maybe?", inside: "Ajjj", money:true, open:false}]
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

{#each data as dt}
<button class="block" on:click={() => dt.open=!dt.open}>
    <p>{dt.title}</p>
</button>
<div>
{#if dt.open}
<div class="inside" transition:slide={{duration:200, delay:100, axis:'y'}}>
    <p in:fly={{duration:400, delay:200, x:-500}}>{dt.inside}</p>
</div>
{/if}
</div>
{/each}