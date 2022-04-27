<script>
import CountryCard from '../component/cards/countryCard.svelte';
import { onMount } from 'svelte';



	let countries = [];

	let search = '';
    

	$: userSearch = countries.filter((c) => c.name.common.toLowerCase().includes(search));

	onMount(async () => {
        let val=localStorage.getItem('countries')
        if (val){
            countries=JSON.parse(val);
        }

        if (!userSearch && !val)
        {
        const res = await fetch(`https://restcountries.com/v3.1/all`);
		countries = await res.json();
        console.log(countries);
        localStorage.setItem('countries', JSON.stringify(countries))
        }
	});

</script>
<div class="main">
    <div class="search-wrapper">
        <h3>Countries</h3>
			<input class="nosubmit" bind:value={search} type="search" placeholder="Search Countries..." />
    </div>
    <div class="countries-wrap">
        {#each userSearch as item }
           <CountryCard country={item}/>
      
        {/each}
        
    
    </div> 
</div>

<style>
.main{
        margin: 1em 5em;
        display: grid;
        gap:1em;
    
    }
    .countries-wrap
    {
        display: grid;
        gap:1em;
		grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));

    }
    .search-wrapper
    {
        display: flex;
        justify-content: space-between;
    }
    input[type='search'] {
		border: none;
		background: transparent;
		margin: 0;
		padding: 7px 8px;
		font-size: 14px;
		color: inherit;
		border: 1px solid transparent;
		border-radius: inherit;
	}

	input[type='search']::placeholder {
		color: #bbb;
	}

    
    
</style>