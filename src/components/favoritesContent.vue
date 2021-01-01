<template>
  <div class="movie-container" v-for="film in favoriteFilms" :key="film.id">
    <div class="image-container">
      <img :src="film.Poster" />
    </div>
    <div class="info">
      <h3 class="title">{{ film.Title }}</h3>
      <p>{{ film.Plot }}</p>
      <div class="action_container col-2">
        <i class="is_favourite fa fa-heart"></i>
        <a
          :href="`https://www.imdb.com/title/${film.imdbID}/`"
          target="_blank"
          class="button ml-1"
          >IMDb</a
        >
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      favoriteFilms: [],
    };
  },
  created() {
    axios.get("http://localhost:3000/films?isFavorite=true").then((response) => {
      this.favoriteFilms = response.data;
    });
  },
};
</script>

<style>
.ml-1 {
  margin-left: 300px;
}
</style>