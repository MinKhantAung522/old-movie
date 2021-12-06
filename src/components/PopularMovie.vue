<template>
  <div>
      
          
  <v-sheet
    class="mx-auto my-auto"
    max-width="100%"
    max-height="100%"
  >
    <v-slide-group
      multiple
      show-arrows
    >
      <v-slide-item
        v-for="movie in movies"
        :key="movie.id"
      >
        <v-card
    class="mx-3"
    max-width="150"
    max-height="300"
  >
    <v-img

      contain
      :src="image_start+movie.poster_path"
    >
    </v-img>
    <v-card-text class="text--primary">
      <h4>{{movie.title }}</h4>
    </v-card-text>
  </v-card>
      </v-slide-item>
    </v-slide-group>
  </v-sheet>

      
  </div>
</template>

<script>
export default {
    props:['movies'],
    data(){
        return{
              model: null,
              image_start: "https://image.tmdb.org/t/p/w500",
        }
    }

}
</script>

<style scoped>
    .popular-box{
        height: 300px;
        width: 100%;
        border: black solid 2px;
        overflow: scroll;
    }
</style>