<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :allMoviesCount="movies.length" :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler"/>
        <AppFilter :updateFilterHeandler="updateFilterHeandler" />
      </div>
      <Box v-if="!movies.length && !isLoader">
        <p class="text-center fs-3 font-bold">Kinolar yo`q</p>
      </Box>
      <Box v-else-if="isLoader" class="d-flex justify-content-center">
        <Loader/>
      </Box>
      <MovieList v-else :movies="onFilterHendler(onSearchHendler(movies, term), filter)" @onToggle="onToggleHandler" @onRemove="onRemoveHendler"/>
      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>

<script>
import AppInfo from '@/components/app-info/AppInfo.vue'
import SearchPanel from '@/components/search-panel/SearchPanel.vue'
import AppFilter from '@/components/app-filter/AppFilter.vue'
import MovieList from '@/components/movie-list/MovieList.vue'
import MovieAddForm from "@/components/movie-add-form/MovieAddForm.vue"
import axios from "axios"
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm
  },
  data() {
    return {
      movies: [],
      term: '',
      filter:'all',
      isLoader: false
    }
  },
  methods: {
    createMovie(items){
      this.movies.push(items)
    },
    onToggleHandler({id ,prop}){
      this.movies = this.movies.map(item => {
        if(item.id === id){
          return{...item, [prop]: !item[prop] }
        }
        return item
      }) 
    },
    onRemoveHendler(id){
      this.movies = this.movies.filter(c => c.id !== id)
    },
    onSearchHendler(arr, term){
      if(term.length == 0){
        return arr
      }
      return arr.filter(c => c.name.toLowerCase().indexOf(term.toLowerCase()) > -1)
    },
    onFilterHendler(arr, filter){
      switch (filter) {
        case 'popular':
          return arr.filter(c => c.like)
        case 'mostViwers':
          return arr.filter(c => c.viewers > 500)
        default:
          return arr
      }
    },
    updateTermHandler(term){
      this.term = term
    },
    updateFilterHeandler(filter){
      this.filter = filter
    },
    async fechData(){
      this.isLoader = true
      try {
      const  res = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
      const newMovies = res.data.map(el => ({
        id: el.id,
        name: el.title,
        like:false,
        favourite:false,
        viewers: el.id * 10
      }))
      this.movies = newMovies
      } catch (error) {
        console.log(error);
      } finally {
        this.isLoader = false
      }
    }
  },
  mounted() {
    this.fechData()
  }
}
</script>

<style>
.app {
  height: 100vh;
  color: #000;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 10px;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, .15);
}
</style>