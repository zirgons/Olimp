<script>
	import { slide, fly, fade } from 'svelte/transition';
    

	export let olimpiadesData = {
	name: "",
	subject: "",
	startingTime: new Date(),
	signingTime: null,
	place: "",
	organizer: "",
	organizersWebsite: "",
	signUpPage: null,
	classes: ""
};
    let open = false;

    function styleDate(date){
		let year = date.getFullYear();
		let month = date.getMonth()+1;
		let day = date.getDate();
		return `${day}.${month}.${year}`
	}
</script>

<style lang=scss>
    $default-color: #858585;
    .block{
        
        height: 50px;
        width: 100%;
        text-align: center;
        background-color: $default-color;
        display: flex ;
        flex-direction: column;
        border-style: solid;
        border-color: black;
        border-radius: 10px;
        border-width: 2px;
        transition: 0.3s;
        margin-top: 10px;
    }
    .block:hover{
        background-color: rgb(136, 136, 136);
    }
    .inside{
        overflow: hidden;
        display: flex;
        box-sizing: border-box;
        width: 98%;
        margin: auto;
        text-align: center;
        background-color: gainsboro; 
        padding: 10px;
        white-space: pre-line;

        border-style: solid;
        border-color: black;
        border-radius: 0px 0px 10px 10px;
        border-width: 0px 2px 2px 2px;
        justify-content: space-evenly;
    }
    
</style>


<div style="display: flex; flex-direction: column;">
    <button transition:slide|global={{duration: 300, delay: 100}}  class="block" on:click={() => open=!open}>
        <h2>{olimpiadesData.name}</h2>
    </button>
    {#if open}
    <div class="inside" transition:slide|global={{duration:300, delay:100, axis:'y'}} >
        <p in:fly={{duration:200, delay:350, x:-500}} out:fly={{duration:400, delay:0, x:-500}}>{olimpiadesData.subject}</p>
        <p in:fly={{duration:200, delay:300, x:-500}} out:fly={{duration:400, delay:50, x:-500}}>{styleDate(olimpiadesData.startingTime)}</p>
        <p in:fly={{duration:200, delay:250, x:-500}} out:fly={{duration:400, delay:100, x:-500}}>{olimpiadesData.place}</p>
        <p in:fly={{duration:200, delay:200, x:-500}} out:fly={{duration:400, delay:150, x:-500}}>{olimpiadesData.classes}</p>
    </div>
    {/if}
    
</div>
