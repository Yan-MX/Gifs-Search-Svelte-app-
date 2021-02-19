<script>
	 let search="";
	 let loading = false
	 let API_url = 'https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=';
	 let gifs= [];

	async function formSubmit (event){
		event.preventDefault();
		loading = true;
		gifs = []
		const url = `${API_url}${search}`
		const res = await fetch(url);
		const json = await res.json();
		console.log(json)
		gifs = json.data.map(gif=> gif.images.fixed_height.url)
		loading = false;
	}
</script>


<style>
	.container{
	margin:10vw
}
.results{
	column-count: 3;
}
</style>
<div class="container">
<form on:submit ={formSubmit}>
	<label for="search">Search</label>
	<input bind:value={search} id = "search" name = "search"/>
	<button type ="submit">Go</button>
</form>

{#if loading}
<img src="https://media2.giphy.com/media/l3nWhI38IWDofyDrW/giphy.gif?cid=790b76115d055ab7424f75514dcb4d7a&rid=giphy.gif" alt="loading">
{/if}

<div class="results">
	{#each gifs as gif}
	<img src={gif} alt="gif">
	{/each}
</div></div>