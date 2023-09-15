<script>
    import OlimpiadesButton from './OlimpiadesButton.svelte';

    let data = [{title: "yup yup", inside: "Some cool data\nSome other cool data\nAnd some more cool data"},
    {title: "Maybe?", inside: "Ajjj"},
    {title: "Baba buji", inside: "Lets goo"}]
</script>



{#each data as dt}
<OlimpiadesButton olimpiadesData={dt}></OlimpiadesButton>
{/each}