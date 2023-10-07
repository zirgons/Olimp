
<script>
    import OlimpiadesButton from '$lib/OlimpiadesButton.svelte';
    import Filter from '$lib/Filter.svelte';
    
    import {olimpiadesData} from './olimpiadesData.js';
    import { slide } from 'svelte/transition';

    

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

<style lang='scss'>
    .month{
        display: flex ;
        flex-direction: column;
        background-color: rgb(236, 236, 236);
        padding: 10px;
        border-radius: 10px;
        margin: 15px;
    }
    .olimpiades{
        padding-left: 30px;
        padding-right: 30px;
        
    }
    ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
        background-color: #333;
        width: 100%;
        height: 48px;
    }

    li {
        float: left;
        border-right: 2px solid #333;

        &.p{
            display: block;
            color: white;
            text-align: center;
            padding: 14px 16px;
            text-decoration: none;
            margin: 0px;
        }
        &:last-child{
            border-right: none;
        }
        & input{
            margin-top: 10px;
            height: 30px;
            background-color:#6e6e6e;
            text-align: left;
            border:none;
        }
    }


    :global(body) { margin: 0; padding: 0; }
</style>

<ul>
    <li><p>Olimpiades</p></li>
    <li><input bind:value={search}></li>
    <li><Filter values={olimpiadesData} bind:filteredData={filter.subjects} filter='subject' name="Priekšmeti"/></li>
    <li><Filter values={olimpiadesData} bind:filteredData={filter.classes} filter='classes' name="Klases"/></li>
</ul>

{#each sortedMonths as month (month[0].startingTime.getFullYear() +". gada "+ month[0].startingTime.toLocaleString('lv', { month: 'long' }))}

    <div class='month' transition:slide={{duration: 200, axis: 'x'}}>
        <h2 transition:slide={{duration: 200}}>{month[0].startingTime.getFullYear() +". gada "+ month[0].startingTime.toLocaleString('lv', { month: 'long' })}</h2>
        <div class='olimpiades'>
            {#each month as data (data.name)}
                <OlimpiadesButton olimpiadesData={data}></OlimpiadesButton>
            {/each}
        </div>
    </div>
{/each}
