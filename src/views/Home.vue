<template>
  <div>
    <h1>Popular Movies and Series</h1>
    <PopularMovie :movies="movies"></PopularMovie>
    <div class="text-center" @click="sent">
      <v-pagination
        v-model="page"
        :length="movies.length"
        :total-visible="5"
        
      ></v-pagination>
    </div>
    <h1>Movies</h1>
    <SingleMovie :movies="movies"></SingleMovie>

  </div>
</template>

<script>
import MovieDetail from '../components/MovieDetail'
import PopularMovie from "../components/PopularMovie";
import SingleMovie from "../components/SingleMovie";
import axios from "axios";
export default {
  components: {
    MovieDetail,
    PopularMovie,
    SingleMovie,
  },
  name: "Home",
  props:["pagee"],

  data() {
    return {
      show: false,
      apikey: "api_key=11f20a2f7d9fda9571965c5ed8d33d4e",
      start: "https://api.themoviedb.org/3",
      movies: [],
      page:this.pagee
    };
  },
  
  methods:{
    sent(){
      let now = this.page;
      this.$emit('pgtran',now)
      this.$router.push("/"+this.page)
    }
  },
  watch: {
    page: function (val) {
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
          
        });
    },
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
        console.log(this.movies);
      }); 
  },
};
</script>
<style scoped>
</style>
