<script lang="ts">
	import Button from '../../components/Button.svelte';
	let movies : any[]= [];
	import { goto } from '$app/navigation';

	const fetchAllMovies = () =>{
		fetch('http://localhost:8000/v1/movies', {redirect: 'follow'})
			.then((response) => response.json())
			.then((result) => {
				movies = result;
			})
			.catch((error) => console.log('error', error));
	}
	const deleteMovie = (id:string) => {
		fetch(`http://localhost:8000/v1/movies/${id}`, {
			method: 'DELETE',
			headers: {
				'Content-Type': 'application/json'
			},
		}).then(
			(response) => {
				if (response.status === 200) {
					fetchAllMovies();
				}
			}
		).catch((error) => console.log('error', error)
		)

	}
fetchAllMovies();
</script>

<main>
	<h1>Movies</h1>
	<div class="grid grid-cols-2 md:grid-cols-3 gap-4">
		{#each movies as movie}
			<div class="max-w-sm rounded overflow-hidden shadow-lg">
				<img class="w-1/2 " src="{movie.poster}" alt="{movie.title}">
				<div class="px-6 py-4">
					<div class="font-bold text-xl mb-2">{movie.title}</div>
					<p class="text-gray-700 text-base">{movie.duration}</p>
				</div>
				<div class="px-6 pt-4 pb-2">
					<span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">#{movie.genre}</span>
				</div>
				<Button class="primary sm" onclick={()=>deleteMovie(movie.id)}>Delete</Button>
				<Button class="primary sm" onclick={()=>deleteMovie(movie.id)}>Put</Button>

			</div>
		{/each}
	</div>
</main>

<Button class="primary sm" onclick={()=>goto('movies/add')}>Post</Button>
