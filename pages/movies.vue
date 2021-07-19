<template>
    <div>
        <NavBar />

        <div class="container">
            <EditModal :movie="selectedMovie" />
            <DeleteModal :movie="selectedMovie" @onDeleted="getAll" />
            
            <h1>
                <MovieEntryModal class="float-right" @onAdd="getAll" />
                Movies
            </h1>

            <table class="table table-boredered">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Movie Name</th>
                        <th>Description</th>
                        <th>Director</th>
                        <th>Country</th>
                        <th>Status</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="movie in movies" :key="movie.id">
                        <td>{{movie.movie_name}}</td>
                        <td>{{movie.description}}</td>
                        <td>{{movie.director}}</td>
                        <td>{{movie.counrty}}</td>
                        <td>{{movie.status}}</td>
                        <td>
                            <b-button @click="onEdit(movie)" variant="info" size="sm">Edit</b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(movie)" variant="danger" size="sm">Delete</b-button>
                        </td>
                    </tr>
                </tbody>

            </table>

        </div>

    </div>
</template>

<script>
export default {
    data() {
        return {
            movies: [],
            selectedMovie: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('http://localhost:8000/api/movies')
            .then((res)=>{
                if(res.status==200) {
                    this.movies = res.data
                    console.log(this.movies)
                }
            })
        },
        onEdit(selectedMovie) {
            this.selectedMovie = selectedMovie;
            this.$bvModal.show('editModal')
        },
        onDelete(selectedMovie) {
            this.selectedMovie = selectedMovie;
            this.$bvModal.show('deleteModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>