<template>
  <div>
    <b-field class="form-base">
      <b-field label="Título">
        <b-input v-model="info.title" placeholder="Digite o título de um filme"></b-input>
      </b-field>
    </b-field>
    <b-field v-if="info.title == ''"></b-field>
    <b-field v-else-if="info.title != ''" label="Ordenar Por">
      <b-select placeholder="Ordenar por" v-model="info.selected">
        <option>Padrão</option>
        <option @click="orderBy(title)">Titulo</option>
      </b-select>
    </b-field>

    <div class="columns is-multiline">
      <movie-card
        v-for="(movie,remFav) in info.movies"
        :key="movie.imdbID"
        :remFav="remFav"
        :movie="movie"
      ></movie-card>
    </div>
  </div>
</template>

<script>
import MovieCard from "@/components/Card";
export default {
  components: {
    MovieCard,
  },
  data() {
    return {
      info: {
        title: "",
        movies: [],
        teste: [],
        selected: "",
      },
    };
  },
  layout: "default",
  methods: {
    getMovies() {
      const key = "d04495fb";
      this.$axios
        .get(`http://www.omdbapi.com/?s=${this.info.title}&apikey=${key}`)
        .then((response) => {
          this.info.movies = response.data.Search;
        });
    },
    orderBy() {
      this.info.movies.sort((a, b) => {
        if (a < b) return -1;
        if (a > b) return 1;
        return 0;
      });
    },
  },
  watch: {
    "info.title": {
      handler() {
        this.getMovies();
      },
    },
    "info.selected": {
      handler() {
        this.orderBy();
      },
    },
  },
};
</script>

<style lang="scss">
.form-base {
  margin-top: 2%;
  margin-bottom: 4%;
}
.columns {
  margin-top: 2%;
}
</style>
