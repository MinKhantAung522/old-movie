<template>
  <div>
    <div v-for="movie in movies" :key="movie.id">
      <div v-if="movie.id ==id">
        <h1>{{movie.id}}</h1>
      </div>
    </div>
  </div>
</template>

<script>
import SingleMovie from "./SingleMovie";
import axios from "axios";
export default {
  components: { SingleMovie },
  props: ["id"],
  data() {
    return {
      apikey: "api_key=11f20a2f7d9fda9571965c5ed8d33d4e",
      start: "https://api.themoviedb.org/3",
      movies: [],
      image_start: "https://image.tmdb.org/t/p/w500",
      page: 1
    };
  },

  watch:{
    page:function(val){
      this.page = val;
      const link =
      this.start +
      "/discover/movie?sort_by=popularity.desc&page=" +
      this.page +
      "&" +
      this.apikey;
    axios  
      .get(link)
      .then((res) => {
        return res.data.results;
      })
      .then((data) => {
        this.movies = data;
        console.log(this.movies);
      });
    }
  },
  mounted() {
    const link =
      this.start +
      "/discover/movie?sort_by=popularity.desc&page=" +
      this.page +
      "&" +
      this.apikey;
    axios
      .get(link)
      .then((res) => {
        return res.data.results;
      })
      .then((data) => {
        this.movies = data;
      });
  },
};
</script>

<style scoped>
.border {
  border: 5px solid black;
}
</style>