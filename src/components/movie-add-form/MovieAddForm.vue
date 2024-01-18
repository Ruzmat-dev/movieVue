<template>
    <div class="movie-add-form" @submit.prevent>
        <h3>Yangi kino qoshish</h3>
        <form class="add-form d-flex">
            <Input class="new-movie-label" placeholder="Qanday kino?" v-model="name"/>
            <Input type="number" class="new-movie-label" placeholder="Nechi marotaba kor`ilgan?" v-model="viewers"/>
            <PrimeryButton class="btn-outline-dark" type="submit" @click="addMovie">Qo`shish</PrimeryButton>
        </form>
    </div>
</template>
<script>
export default {
    data() {
        return {
            name: "",
            viewers: ""
        }
    },
    methods: {
        addMovie() {
            if(!this.name || !this.viewers) return
            const newMovie = {
                id: Date.now(),
                name: this.name,
                viewers: this.viewers,
                favourite: false,
                like: false
            }
            this.$emit("createMovie" , newMovie)
            this.name= ''
            this.viewers = ''
        }   

    }
}
</script>
<style scoped>
.movie-add-form {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, .15);
}
</style>