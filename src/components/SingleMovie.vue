<template>
  <div>
    <v-row>
      <v-col md="3" cols="4" v-for="movie in movies" :key="movie.id">
        <v-card class="mx-auto" max-width="250" max-height="500" @click="displayEach(movie.id)">
          <v-img
            width="100%"
            height="100%"
            :src="image_start+movie.poster_path"
          >
                  
            <v-card-text
          class="rate">rating</v-card-text>
          </v-img>
          <div class="detail">
            <v-card-title>
              <h4>{{movie.title}}</h4>
            </v-card-title>
          </div>
        </v-card>
      </v-col>
    </v-row>    
  </div>
</template>

<script>
import MovieDetail from './MovieDetail'
export default {
  components: { MovieDetail },
  props: ["movies"],
  data(){
      return{
          image_start: "https://image.tmdb.org/t/p/w500",
          page: 1,
      }
  },
  methods:{
    displayEach(id,page){
      this.$router.push('/movie-detail/'+id)
    }
  }
};
</script>

<style>
.detail{
width: 250px;
height:90px;
background: rgb(208, 238, 238);
}
.rate{
  display: inline;
  background: black;
  color: aqua;
  border-radius: 20px;
  margin-bottom: 49px;
}
</style>