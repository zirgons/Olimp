<script>
    export let values
    export let selected = []
    export let onchange = (_) => {}

    const select = (i) => {
        console.log({sel: i})
        onchange([...selected, i] )
    }

    const unselect = (i) => {
        console.log({unsel: i})
        onchange(selected.filter(v => v != i) )
    }


</script>

<div class="filter">
  <button class="flt-item --unselected" on:click={() => onchange([])}>VISI</button>
{#each values as v}

  {#if selected.includes(v)}
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