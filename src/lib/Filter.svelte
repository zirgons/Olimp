<script>
    export let values
    export let filteredData = [];
    export let filter;

    const unique = (rs) => {
        return Array.from(new Set(rs))
    }

    const items = unique(values.map(o => o[filter]));

    const select = (i) => {
        console.log({sel: i})
        onchange([...filteredData, i] )
    }

    const unselect = (i) => {
        console.log({unsel: i})
        onchange(filteredData.filter(v => v != i) )
    }

    const onchange = (v) => {
        filteredData = v
    }
</script>

<div class="filter">
  <button class="flt-item --unselected" on:click={() => onchange([])}>VISI</button>
    {#each items as v}

    {#if filteredData.includes(v)}
        <button class="flt-item --selected" on:click={() => unselect(v)}>{ v }</button>
    {:else}
        <button class="flt-item --unselected" on:click={() => select(v)}>{ v }</button>
    {/if}

    {/each}
</div>

<style>
    .filter {
        display: flex;
        flex-direction: row;
        gap: 1em;
        flex-wrap: wrap;
    }
    .flt-item {
        all: initial;
        cursor: pointer;
    }
    .flt-item.--selected {
        border-bottom: 1px solid #999;
        font-weight: bold;

    }
    .flt-item.--unselected {
        border-bottom: 1px dashed #999;

    }
</style>