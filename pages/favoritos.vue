<template>
  <div>
    <div class="titleFav">
      <h2>FAVORITOS</h2>
    </div>
    <div class="columns is-multiline">
      <div v-for="(favorito, fav) in favoritos" :key="favorito.id" class="column is-3">
        <div class="card">
          <div class="card-image">
            <figure class="image is-4by3">
              <img :src="favorito.poster" />
            </figure>
          </div>
          <div class="card-content">
            <div class="media">
              <div class="media-content">
                <p class="title is-4">{{favorito.title}}</p>
              </div>
            </div>

            <div class="content">
              <b-button @click="removeMovie(fav)" type="is-danger">Remover</b-button>
              <a :href="`movie/${favorito.id}`">
                <b-button type="is-success">Visualizar</b-button>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      favoritos: [],
    };
  },
  methods: {},
  mounted() {
    if (localStorage.getItem("titleFav")) {
      try {
        this.favoritos = JSON.parse(localStorage.getItem("titleFav"));
      } catch (e) {
        localStorage.removeItem("titleFav");
      }
    }
  },
  methods: {
    removeMovie(x) {
      this.favoritos.splice(x, 1);
      this.saveFav();
    },
    saveFav() {
      const parsed = JSON.stringify(this.favoritos);
      localStorage.setItem("titleFav", parsed);
    },
  },
};
</script>

<style lang="scss">
.titleFav {
  text-align: center;
  margin-top: 4%;
  margin-bottom: 4%;
  font-weight: bold;
  font-size: 3em;
}
.card {
  .card-image {
    figure {
      height: 35vh;
    }
  }
  .card-content {
    .media {
      .media-content {
        .title {
          text-align: center;
          font-size: 20px;
        }
      }
    }
    .content {
      text-align: center;
    }
  }
}
</style>