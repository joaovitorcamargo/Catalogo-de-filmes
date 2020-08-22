<template>
  <b-navbar class="nav">
    <template slot="brand">
      <b-navbar-item tag="router-link" :to="{ path: '/' }"
        ><b>Teste Catalogo Filmes</b></b-navbar-item
      >
    </template>
    <template slot="start">
      <b-navbar-item href="#">Home</b-navbar-item>
      <b-navbar-item href="#">Favoritos</b-navbar-item>
    </template>
    <Nuxt />
  </b-navbar>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          to: { name: "index" }
        }
      ]
    };
  }
};
</script>
<style lang="scss">
.nav {
  -webkit-box-shadow: 0px 3px 5px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 0px 3px 5px 0px rgba(0, 0, 0, 0.75);
  box-shadow: 0px 3px 5px 0px rgba(0, 0, 0, 0.75);
}
</style>
