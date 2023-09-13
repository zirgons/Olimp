<script>
    import OlimpiadesButton from './OlimpiadesButton.svelte';

    const data = [{title: "yup yup", inside: "Some cool data\nSome other cool data\nAnd some more cool data"},
    {title: "Maybe?", inside: "Ajjj"},
    {title: "Maybe 2?", inside: "Ajjj2"}]
    let search = '';

</script>


<input bind:value={search}>

{#each data as dt}
    {#if dt.title.toLowerCase().includes(search.toLowerCase())}
        <OlimpiadesButton olimpiadesData={dt}></OlimpiadesButton>
    {/if}
{/each}
