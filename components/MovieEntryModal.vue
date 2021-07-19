<template>
    <div>
        <b-button v-b-modal.movieEntryModal class="btn btn-info">Add Movie</b-button>

        <b-modal id="movieEntryModal" title="Movie Entry" ok-title="Save" @ok="onSubmit">
            <form action="#" ref="form">
                <b-form-group
                    label="Movie Name"
                    label-for="movie_name"
                    >
                    <b-form-input id="movie_name" v-model="movie.movie_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Description"
                    label-for="description"
                    >
                    <b-form-input id="description" v-model="movie.description" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Director"
                    label-for="director"
                    >
                    <b-form-input id="director" v-model="movie.director" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Country"
                    label-for="counrty"
                    >
                    <b-form-input id="counrty" v-model="movie.counrty" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Rating"
                    label-for="rating"
                    >
                    <b-form-input id="rating" type="number" v-model="movie.rating" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Status"
                    label-for="status"
                    >
                    <b-form-select id="status" v-model="movie.status" :options="statuses"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return {
            movie: {},
            statuses: [
                { value: 'good', text: 'Good' },
                { value: 'very goog', text: 'Very Good' },
                { value: 'excellent', text: 'Excellent' },
                { value: 'bad', text: 'Bad' },
                { value: 'very bad', text: 'Very Bad' },
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.post('http://localhost:8000/api/movies', this.movie)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added the movie')
                    this.$emit('onAdd')
                }
            })
        }
    }
    
}
</script>