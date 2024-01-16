<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :allMoviesCount="movies.length" :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler"/>
        <AppFilter />
      </div>
      <MovieList :movies="onSearchHendler(movies, term)" @onToggle="onToggleHandler" @onRemove="onRemoveHendler"/>
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
      movies: [
        {
          name: 'Ruzmat',
          viewers: 811,
          favourite: false,
          like: true,
          id:1,
        },
        {
          name: 'Empier of osman',
          viewers: 411,
          favourite: true,
          like: true,
          id:2,
        },
        {
          name: 'Ertugrul',
          viewers: 711,
          favourite: true,
          like: false,
          id:3,
        }
      ],
      term: ''
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
    updateTermHandler(term){
      this.term = term
    }
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