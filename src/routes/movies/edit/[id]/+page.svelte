<script lang="ts">
    import Button from '../../../../components/Button.svelte';
    import {page} from "$app/stores";

    let formData = {
        title: '',
        genre: '',
        duration: '',
        poster: '',
    };
    const fetchAMovieById = async (id:any) => {
        fetch( 'http://localhost:8000/v1/movies/'+id)
            .then(response => response.json())
            .then(data => {
                formData = data;
            });
    }

    const submitForm = () => {
        if (formData.title === '') {
            alert('Title is required');
            return;
        }
        if (formData.genre === '') {
            alert('genre is required');
            return;
        }
        if (formData.duration === '') {
            alert('Duration is required');
            return;
        }
        if (formData.poster === '') {
            alert('Poster is required');
            return;
        }
        fetch(
            'http://localhost:8000/v1/movies',
            {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(formData)
            }
        ).then(() => {
                formData = {
                    title: '',
                    genre: '',
                    duration: '',
                    poster: '',
                };
                alert('Movie added successfully');
                window.location.href = '/movies';
            }
        )
    };
</script>

<div>
    <h3>Update Movie</h3>
    <div class="form-movie">
        <div class="form-input">
            <label for="title">Title</label>
            <input type="text" id="title" name="title" bind:value={formData.title} placeholder="Title"/>
        </div>
        <div class="form-input">
            <label for="genre">Genre</label>
            <input type="text" id="genre" bind:value={formData.genre} name="genre" placeholder="genre"/>
        </div>
        <div class="form-input">
            <label for="duration">Duration</label>
            <input type="text" id="duration" bind:value={formData.duration} name="genre" placeholder="genre"/>
        </div>
        <div class="form-input">
            <label for="poster">Poster</label>
            <input type="text" id="poster" bind:value={formData.poster} name="genre" placeholder="genre"/>
        </div>
        <Button onclick={submitForm} >Save</Button>
    </div>
</div>
