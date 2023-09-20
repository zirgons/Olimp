<script>
    export let values
    export let filteredData = [];
    export let filter;
    export let name;
    let open = false;

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

<svelte:window on:click={(event) =>{
    if(!event.target.classList.contains('flt-item') && !event.target.classList.contains('dropdown-content') && !event.target.classList.contains(name)){
        open=false;
    }
}} />

<div>
    <button on:click={()=>{ open = !open}} class="dropbtn {name}">{open ? "▲" : "▼"}{name}</button>
    {#if open}
        <div class='dropdown-content'>
            <button class="flt-item --unselected" on:click={() => onchange([])}>VISI</button>
            {#each items as v}
        
                {#if filteredData.includes(v)}
                    <button class="flt-item --selected" on:click={() => unselect(v)}>{ v }</button>
                {:else}
                    <button class="flt-item --unselected" on:click={() => select(v)}>{ v }</button>
                {/if}
        
            {/each}
        </div>
    {/if}
</div>

<style lang="scss">
    .flt-item {
        all: initial;
        cursor: pointer;
        position: relative;
        padding:1px;

        &.--selected {
            font-weight: bold;
        }
    }
    .dropdown-content {
        display: flex ;
        flex-direction: column;
        position: absolute;
        background-color: #f1f1f1;
        min-width: 160px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        z-index: 1;
    }
    .dropbtn{
        cursor: pointer;
        height: 30px;
        background-color:#e3e3e3;
        border: none;
        min-width: 160px;
        text-align: left;
        border-radius: 5px;
        margin-top: 10px;
    }
</style>