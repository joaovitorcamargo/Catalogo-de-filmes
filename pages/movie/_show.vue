<template>
  <div>
    <p>{{info.Title}}</p>
    <img :src="info.Poster" alt />
    <p>{{info.Year}}</p>
    <p>{{info.Released}}</p>
    <p>{{info.Plot}}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      info: "",
    };
  },
  created() {
    return console.log(this.$route.params.show);
  },
  mounted() {
    this.showMovie();
  },
  methods: {
    showMovie() {
      const key = "d04495fb";
      this.$axios
        .get(
          `http://www.omdbapi.com/?i=${this.$route.params.show}&apikey=${key}`
        )
        .then((response) => {
          this.info = response.data;
        });
    },
  },
};
</script>

<style>
</style>