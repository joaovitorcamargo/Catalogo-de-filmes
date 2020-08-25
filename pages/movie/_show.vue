<template>
  <div>
    <div class="columns movie">
      <div class="column">
        <div class="poster">
          <img :src="info.Poster" alt />
        </div>
      </div>
      <div class="column">
        <div class="info">
          <h2 class="titleMovie">{{info.Title}}</h2>
          <p>
            <b>Ano de Lançamento:</b>
            {{info.Released}}
          </p>
          <p class="description">
            <b>Sinopse:</b>
            {{info.Plot}}
          </p>
          <p>
            <b>Country Origin:</b>
            {{info.Country}}
          </p>
          <p>
            <b>Awards:</b>
            {{info.Awards}}
          </p>
          <p>
            <b>Actors:</b>
            {{info.Actors}}
          </p>
          <p>
            <b>Writer:</b>
            {{info.Writer}}
          </p>
          <p>
            <b>Runtime:</b>
            {{info.Runtime}}
          </p>
        </div>
      </div>
    </div>
    <hr />
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

<style lang="scss">
.movie {
  margin-top: 4%;

  .column {
    padding: 2%;
    .poster {
      text-align: center;
      float: right;
    }
    .info {
      float: left;
      padding: 10%;
      display: grid;
      justify-content: center;
      align-items: center;
      text-align: justify;
      .titleMovie {
        font-size: 2em;
      }
      .description {
        margin-top: 4%;
      }
    }
  }
}
@media only screen and (max-width: 600px) {
  .movie {
    .column {
      .poster {
        text-align: center;
        float: none;
      }
      .info {
        padding-left: 10%;
        padding-right: 10%;
        padding-top: 0;
        display: grid;
        justify-content: center;
        align-items: center;
        text-align: justify;
        .titleMovie {
          font-size: 2em;
          text-align: center;
        }
        .description {
          margin-top: 4%;
        }
      }
    }
  }
}
</style>