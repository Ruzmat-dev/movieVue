<template >
    <div class="btn-group">
        <button v-for="btn in filterButtons" :key="btn.name" class="btn" :class="[filter == btn.name ? 'btn-dark' : 'btn-outline-dark']" @click="filterHeander(btn.name)">{{ btn.title }}</button>
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
            filterButtons: [
                {
                    id:1,
                    title: "Barcha kinolar",
                    name: "all"
                },
                {
                    id:2,
                    title: "Mashhur kinolar",
                    name: "popular"
                },
                {
                    id:3,
                    title: "Eng kop korilgan kinolar",
                    name: "mostViwers"
                }
            ],
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