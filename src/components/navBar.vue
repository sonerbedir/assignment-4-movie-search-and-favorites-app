<template>
  <div class="header-width">
    <header>
      <ul>
        <li>
          <router-link to="/">
            <a>Anasayfa</a>
          </router-link>
        </li>
        <li>
          <router-link to="/favorites">
            <a>Favorilerim</a>
          </router-link>
        </li>
      </ul>
      <span> Movie App With Vue </span>
    </header>
  </div>
</template>
<style >
.header-width {
  width: 100%;
}
</style>
<script>
export default {};
</script>