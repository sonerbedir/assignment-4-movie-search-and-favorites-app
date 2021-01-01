<template>
  <div v-for="filmItem in items" :key="filmItem.id" class="movie-container">
    <div class="image-container">
      <img :src="filmItem.Poster" />
    </div>
    <div class="info">
      <h3 class="title">{{ filmItem.Title }}</h3>
      <p>{{ filmItem.Plot }}</p>
      <div class="action_container">
        <i @click="favoriteAdded(filmItem)" :class="{'is_favourite': filmItem.isFavorite }" class="fa fa-heart"></i>
        <a
          :href="`https://www.imdb.com/title/${filmItem.imdbID}/`"
          target="_blank"
          class="button ml-2"
          >IMDb</a
        >
        <button @click="removeItem(filmItem.id)" type="button" class="button">
          Kaldır
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  props: ["items"],

  data() {
    return {
      favoritesFilm: [],
      isFavorite: false,
    };
  },
  methods: {

    favoriteAdded(item) {
      item.isFavorite=true;
      axios.patch(`http://localhost:3000/films/${item.id}`,item).then((response) => {
        console.log(response.data);
        // this.favoritesFilm=response.data;

      });
    },
    removeItem(id) {
      axios.delete(`http://localhost:3000/films/${id}`).then((response) => {
        this.$emit("succesfully-deleted", id);
      });
    },
  },
};
</script>

<style >
.ml-2 {
  margin-left: 180px;
}
</style>