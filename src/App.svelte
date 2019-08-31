<script>
	let search = '';
	let loading = false;
	const API_URL = 'https://api.giphy.com/v1/gifs/search?api_key=JnxTmEGKXjZeUKBzRjTQoMDg8OX8pS5U&rating=pg&q=';

	let gifs = [];

	async function formSubmit(event) {
		event.preventDefault();

		loading = true;

		gifs = [];

		const url = `${API_URL}${search}`;

		const response = await fetch(url);

		const data = await response.json();

		gifs = data.data.map(gif => gif.images.fixed_height.url);
		
		search = '';
		loading = false;

	}
	
</script>

<style>
	.results {
		column-count: 3;
	}
	img {
		width: 100%;
		height: auto;
	}
</style>

<form on:submit={formSubmit}>
	<label for='search'>Search</label>
	<input bind:value={search} id="search" name="search" autocomplete="off">
	<button type="submit">GO!</button>
</form>

{#if loading}
	<img src="https://media.giphy.com/media/52qtwCtj9OLTi/giphy.gif" alt="loading">
{/if}

<div class="results">
	{#each gifs as gif}
		<img src={gif} alt="gif">
	{/each}
</div>