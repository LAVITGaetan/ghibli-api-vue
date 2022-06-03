<template>
  <div id="app">
    <div class="modal" v-if="film.length > 0"><li v-for="film in film" :key="film.id"> {{film.title}}</li></div>
    <h1 class="title">Ghibli Movies</h1>
    <div class="flex" v-if="films.length > 0">
      <div class="card" v-for="film in films" :key="film.id">
        <img class="card-thumbnail" v-bind:src="film.image" v-bind:alt="film.title" />
        <div class="card-action" @click="showMovie(film.id)">+</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_uri: "https://ghibliapi.herokuapp.com/films",
      films: {},
      film: []
    };
  },
  methods: {
    fetchApi() {
      fetch(this.api_uri)
        .then((res) => {
          return res.json();
        })
        .then((data) => {
          this.films = data;
        });
    },
    showMovie(movieId) {
      this.film = [];
      let film = this.films.find(movie => movie.id == movieId);
      this.film.push(film);
      console.log(this.film[0]);
    }
  },
  beforeMount() {
    this.fetchApi();
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background: #f5fafb;
}

.modal {
  position: fixed;
  width: 300px;
  height: fit-content;
  padding: 50px;
  background: #ffffff;
  box-shadow: 5px 5px 100px 10px #00000050;
  top: 25vh;
  z-index: 1000;
  left: calc(50vw - 150px);
}

.title {
  font-size: 30px;
  color: #181826;
  text-align: center;
  padding: 2em 25% 0 25%;
  font-weight: bold;
}

.flex {
  display: flex;
  justify-content: space-evenly;
  padding: 2em 10%;
  flex-wrap: wrap;
}

.card {
  width: 300px;
  height: 450px;
  margin: 50px;
  position: relative;
  border-radius: 5px;
}

.card-action {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 5px 5px 10px 1px #00000020;
  z-index: 100;
  width: 150px;
  height: 64px;
  background: #13e4e4ea;
  color: #fff;
  font-size: 30px;
  font-weight: bold;
  border-radius: 50px;
  cursor: pointer;
  left: calc(50% - 75px);
  bottom: -32px;
}

.card-action:hover {
  transition: .3s ease;
  background: #13E4E4;
}

.card-thumbnail {
  width: 300px;
  border-radius: 5px;
  height: 450px;
}
</style>
