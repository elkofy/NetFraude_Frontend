<script>
	import { onMount } from 'svelte';
	import Button from '../components/Button.svelte';
	let movies = [];
	function Onbuttonclick() {
		var requestOptions = {
			method: 'GET',
			redirect: 'follow'
		};

		fetch('http://localhost:8000/v1/movies', requestOptions)
			.then((response) => response.json())
			.then((result) => {
				movies = result;
			})
			.catch((error) => console.log('error', error));
	}
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<Button class="primary sm" onclick={Onbuttonclick}>GET</Button>

<main>
	<h1>Whiskey Drinks Menu</h1>
	<ul>
		{#each movies as movie}
			<li>{movie.title}</li>
		{/each}
	</ul>
</main>

<Button class="primary sm" onclick={Onbuttonclick}>Post</Button>
<Button class="primary sm" onclick={Onbuttonclick}>Put</Button>
<Button class="primary sm" onclick={Onbuttonclick}>Delete</Button>
