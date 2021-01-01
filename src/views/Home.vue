<template>
  <div>
    <div id="app">
      <input
        v-model="filmName"
        @keypress.enter="getFilms"
        type="text"
        autofocus
        placeholder="Film adını yazın ve enter tuşuna basın..."
        class="search_text"
      />
      <div id="movies">
        <film-content :items="filmList" @succesfully-deleted="deleteFromList" />
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import filmContent from "@/components/filmContent";
export default {
  components: {
    filmContent,
  },
  data() {
    return {
      filmList: [],
      filmName: null,
      foundedFilm: {},
    };
  },
  created() {
    axios.get("http://localhost:3000/films").then((response) => {
      this.filmList = response.data;
    });
  },
  methods: {
    getFilms() {
      axios
        .get(
          `http://www.omdbapi.com/?i=tt3896198&apikey=d8b18990&t=${this.filmName}`
        )
        .then((filmResponse) => {
          if (filmResponse.data.Response !== "False") {
            this.foundedFilm = filmResponse.data;
          }
        })
        .then(() => {
          console.log(this.foundedFilm);
          if (
            this.foundedFilm &&
            this.foundedFilm.hasOwnProperty("imdbID") &&
            !this.filmList.find((x) => x.imdbID === this.foundedFilm.imdbID)
          ) {
            this.foundedFilm.isFavorite=false;
            axios
              .post(`http://localhost:3000/films`, this.foundedFilm)
              .then((response) => {
                this.filmList.push(response.data);
              });
          }
        });
    },
    deleteFromList(id) {
      this.filmList = this.filmList.filter((x) => x.id !== id);
    },
  },
};
</script>


<style>
</style>