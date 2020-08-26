<template>
  <div class="column is-3">
    <div class="card">
      <div class="card-image">
        <figure class="image is-4by3">
          <img :src="movie.Poster" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{movie.Title}}</p>
          </div>
        </div>

        <div class="content">
          <b-button v-if="isFav" @click="addFav()" type="is-success">Favoritar</b-button>
          <a v-else href="/favoritos">
            <b-button type="is-info">Ver Favoritos</b-button>
          </a>
          <a :href="`movie/${movie.imdbID}`">
            <b-button type="is-warning">Visualizar</b-button>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "movie",
  props: ["movie", "selected"],
  data() {
    return {
      titleFav: [],
    };
  },
  mounted() {
    this.loadFav();
  },
  computed: {
    isFav() {
      if (
        this.titleFav.find((movie) => {
          return movie.id == this.movie.imdbID;
        })
      ) {
        return false;
      }
      return true;
    },
  },
  methods: {
    addFav() {
      this.loadFav();
      this.titleFav.push({
        id: this.movie.imdbID,
        title: this.movie.Title,
        poster: this.movie.Poster,
      });
      this.saveFav();
    },
    loadFav() {
      if (localStorage.getItem("titleFav")) {
        try {
          this.titleFav = JSON.parse(localStorage.getItem("titleFav"));
        } catch (e) {
          localStorage.removeItem("titleFav");
        }
      }
    },
    saveFav() {
      const parsed = JSON.stringify(this.titleFav);
      localStorage.setItem("titleFav", parsed);
    },
    removeMovie(x) {
      this.loadFav();
      this.titleFav.splice(x, 1);
      this.saveFav();
    },
    orderBy() {
      alert("dsadsa");
    },
  },
  watch: {
    selected: {
      handler() {
        this.orderBy();
      },
    },
  },
};
</script>

<style lang="scss">
</style>