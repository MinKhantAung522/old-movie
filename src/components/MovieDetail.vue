<template>
  <div>
    <div v-if="false">
      <button @click="back">BACK</button>
    </div>
    <div v-for="movie in filtermovies" :key="movie.id">
      <h1>{{ movie.title }}</h1>
      <div class="d-flex flex-row border">
        <div>
          <v-img
            class="white--text align-end"
            width="100%"
            height="100%"
            max-width="250"
            max-height="350"
            :src="image_start + movie.poster_path"
          >
          </v-img>
        </div>
        <div class="ms-4">
          <h2>Overview</h2>
          <p>{{ movie.overview }}</p>
          <h2>Release Date</h2>
          <p>{{ movie.release_date }}</p>
          <h2>User Rating</h2>
          <p>
            {{ movie.vote_average }}({{ movie.vote_count }} people like this)
          </p>
          <v-btn color="error" rounded x-large>Download</v-btn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SingleMovie from "./SingleMovie";
import axios from "axios";
export default {
  components: { SingleMovie },
  props: ["id", "pagee"],
  data() {
    return {
      apikey: "api_key=11f20a2f7d9fda9571965c5ed8d33d4e",
      start: "https://api.themoviedb.org/3",
      movies: [],
      image_start: "https://image.tmdb.org/t/p/w500",
    };
  },
  methods:{
    back(){
      this.$emit("pgchg",this.pagee)
      this.$router.push('/'+this.pagee);
    }
  },
  computed: {
    filtermovies() {
      return this.movies.filter((movie) => {
        return movie.id == this.id;
      });
    },
  },  
  mounted() {
    const link =
      this.start +
      "/discover/movie?sort_by=popularity.desc&page=" +
      this.pagee +
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