
<script>
    import OlimpiadesButton from './OlimpiadesButton.svelte';
    import {olimpiadesData} from './olimpiadesData.js';
    import { slide } from 'svelte/transition';
    olimpiadesData.sort(function(a,b){
		  return new Date(a.startingTime).valueOf() - new Date(b.startingTime).valueOf();
	});
    let months = {};
    let search = '';
    let sortedMonths;
    $: {
        let months = {};
        olimpiadesData.forEach((e) => {
            if(!e.name.toLowerCase().includes(search.toLowerCase())){
                return;
            }
                
            let startingMonth = e.startingTime.getMonth();
            let startingYear = e.startingTime.getFullYear();
            if(!months[startingMonth+startingYear]) months[startingMonth+startingYear] = [];
            months[startingMonth+startingYear].push(e);
        })
        sortedMonths = Object.values(months).sort(function(a,b){
            return new Date(a[0].startingTime).valueOf() - new Date(b[0].startingTime).valueOf();
        });
        console.log(sortedMonths);
    }
    
    

</script>

<style>
    .month{
        display: flex ;
        flex-direction: column;
        background-color: rgb(236, 236, 236);
        margin-top: 10px;
        padding: 10px;
        border-radius: 10px;
    }
    .olimpiades{
        padding-left: 30px;
        padding-right: 30px;
    }
</style>

<input bind:value={search}>

{#each sortedMonths as month (month[0].startingTime.getFullYear() +". gada "+ month[0].startingTime.toLocaleString('lv', { month: 'long' }))}

    <div class='month' >
        <h2 transition:slide={{duration: 200}}>{month[0].startingTime.getFullYear() +". gada "+ month[0].startingTime.toLocaleString('lv', { month: 'long' })}</h2>
        <div class='olimpiades'>
            {#each month as data (data.name)}
                <OlimpiadesButton olimpiadesData={data}></OlimpiadesButton>
            {/each}
        </div>
    </div>
    
{/each}
