<template>
  <div>
    <!-- <header>
      <ul>
        <li>
          <a href="./index.html">Anasayfa</a>
        </li>
        <li>
          <a href="./favorites.html" class="active">Favorilerim</a>
        </li>
      </ul>
      <span> Movie App | kablosuzkedi </span>
    </header> -->
    <div id="app">
      <div id="movies">
       <favorites-content/>
      </div>
    </div>
  </div>
</template>

<script>
import favoritesContent from "@/components/favoritesContent";
export default {
  
  components:{

    favoritesContent
  }
}
</script>