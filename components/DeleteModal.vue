<template>
    <div>

        <b-modal id="deleteModal" title="Delete Movie" ok-title="Save" @ok="onDelete" ok-variant="danger">
            Are You Sure Want to delete this?
            <br>
            <br>
            <h1>{{movie.movie_name}}</h1>
        </b-modal>

    </div>
</template>

<script>
export default {
    props: {
        movie: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('http://localhost:8000/api/movies/' + this.movie.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Movie is deleted Successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
    
}
</script>