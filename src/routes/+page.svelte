
<script>
    import OlimpiadesButton from './OlimpiadesButton.svelte';
    import {olimpiadesData} from './olimpiadesData.js';
    import { slide } from 'svelte/transition';

    import Filter from '../lib/Filter.svelte'

    olimpiadesData.sort(function(a,b){
		  return new Date(a.startingTime).valueOf() - new Date(b.startingTime).valueOf();
	});

    let filter = { subjects: [], classes: [] }

    const filterMatch = (filter, entry) => {
        if (filter.subjects.length && ! filter.subjects.includes(entry.subject)) return false
        if (filter.classes.length && ! filter.classes.includes(entry.classes)) return false
        return true
    }
    
    let months = {};
    let search = '';
    let sortedMonths;
    $: {
        let months = {};
        olimpiadesData.forEach((e) => {

            if ( ! filterMatch(filter, e)) return 

            if(!e.name.toLowerCase().includes(search.toLowerCase())){
                return;
            }
                
            let key = e.startingTime.getMonth()+e.startingTime.getFullYear();
            if(!months[key]) months[key] = [];
            months[key].push(e);
        })
        sortedMonths = Object.values(months).sort(function(a,b){
            return new Date(a[0].startingTime).valueOf() - new Date(b[0].startingTime).valueOf();
        });
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

<Filter values={olimpiadesData} bind:filteredData={filter.subjects} filter='subject' />
<Filter values={olimpiadesData} bind:filteredData={filter.classes} filter='classes' />
<br>

{#each sortedMonths as month (month[0].startingTime.getFullYear() +". gada "+ month[0].startingTime.toLocaleString('lv', { month: 'long' }))}

    <div class='month' transition:slide={{duration: 100, axis: 'x'}}>
        <h2 transition:slide={{duration: 200}}>{month[0].startingTime.getFullYear() +". gada "+ month[0].startingTime.toLocaleString('lv', { month: 'long' })}</h2>
        <div class='olimpiades'>
            {#each month as data (data.name)}
                <OlimpiadesButton olimpiadesData={data}></OlimpiadesButton>
            {/each}
        </div>
    </div>
{/each}