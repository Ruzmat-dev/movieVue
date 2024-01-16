<template >
    <div class="btn-group">
        <button class="btn" type="button" @click="filterHeander('all')" :class="[filter === 'all' ? 'btn-dark' : 'btn-outline-dark']">Barcha kinolar</button>
        <button class="btn" type="button" @click="filterHeander('popular')" :class="[filter === 'popular' ? 'btn-dark' : 'btn-outline-dark']">Mashhur kinolar</button>
        <button class="btn" type="button" @click="filterHeander('mostViwers')" :class="[filter === 'mostViwers' ? 'btn-dark' : 'btn-outline-dark']">Eng kop korilgan kinolar</button>
    </div>
</template>
<script>
export default {
    props: {
        updateFilterHeandler: {
            type: Function,
            required: true,
        },
        filterName: {
            type: String,
            required: true,
        }
    },
    data(){
        return{
            filter: 'all'
        }
    },
    methods: {
        filterHeander(filter) {
            this.filter = filter
            this.updateFilterHeandler(this.filter)
        }
    }
}
</script>
<style scoped>
    
</style>