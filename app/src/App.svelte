<script>
	export let search='';
	let loading = false;
	let gifs = [];
	async function formSubmitted(event){
		event.preventDefault();
		loading = true;
		gifs = [];
		const API_URL ='https://api.giphy.com/v1/gifs/search?api_key=Fe31AzvztP12NLIxF6mnBLG2s9qEAq44&rating=pg&q=';
		const url = `${API_URL}${search}`;
		const response= await fetch(url);
		const json = await response.json();
		
		gifs = json.data.map(gif => gif.images.fixed_height.url);
		loading = false;
		console.log(gifs);





	}




</script>

<main>
</main>

<style>

.results {
	column-count: 3;
}

img {
	width: 100%;
	height: auto;
}
	

</style>

<form on:submit={formSubmitted}>
	<label for="search"> Search </label>
	<input bind:value={search} id="search" name="search"/>
	<button type="submit"> GO</button>

</form>


{#if loading}

    <img alt="loading" src="https://media2.giphy.com/media/l3nWhI38IWDofyDrW/giphy.gif?cid=790b76115d055ab7424f75514dcb4d7a&rid=giphy.gif" />

{/if}

<div class="results">
	{#each gifs as gif}
		<img alt="gif" src={gif} />
	{/each}
</div>

