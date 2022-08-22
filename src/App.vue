<template>
  <div>
    <SearchBar placeholder="cerca film" @search="startSearch"></SearchBar>
    <section id="movies">
      <h2>movies</h2>
      <ul v-for="movie in movies" :key="movie.id">
        <li>{{ movie.title }}</li>
        <li>{{ movie.original_title }}</li>
        <li>{{ movie.original_language }}</li>
        <li>{{ movie.vote_average }}</li>
      </ul>
    </section>
    <section id="series">
      <h2>series</h2>
      <ul v-for="serie in series" :key="serie.id">
        <li>{{ serie.name }}</li>
        <li>{{ serie.original_name }}</li>
        <li>{{ serie.original_language }}</li>
        <li>{{ serie.vote_average }}</li>
      </ul>
    </section>
   
  </div>
</template>
 
<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
export default {
  components: { SearchBar },
  data() {
    return {
      movies: [],
      series:[],
      api: {
        language: "it",
        key: "fc1383bffc985a009aa4698df58ddc3e",
        baseUri: "https://api.themoviedb.org/3",
      },
    };
  },
  methods: {
    startSearch(query) {
      const { language, key, baseUri } = this.api;
      
       const config = {
        params: {
          api_key: key,
          language: language,
          query: query,
        },
      };

      axios.get(`${baseUri}/search/movie`, config).then((res) => {
        this.movies = res.data.results;
      });
      axios.get(`${baseUri}/search/tv`, config).then((res) => {
        this.series = res.data.results;
      });

      


     
    },
  }, 
};
</script>

<style>
</style> 