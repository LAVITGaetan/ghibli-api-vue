<template>
  <div id="app">
    <div class="modal" v-if="film.length > 0">
      <h3 class="modal-title" v-for="film in film" :key="film.id">
        {{ film.title }}
      </h3>
      <ul class="modal-list">
        <li v-for="film in film" :key="film.id">{{ film.original_title_romanised }}</li>
        <li v-for="film in film" :key="film.id">{{ film.original_title }}</li>
        <li v-for="film in film" :key="film.id">{{ film.producer }}</li>
        <li v-for="film in film" :key="film.id">{{ film.release_date }}</li>
      </ul>
      <div @click="resetMovie" class="modal-close">Fermer</div>
    </div>
    <h1 class="title">Ghibli Movies</h1>
    <div class="flex" v-if="films.length > 0">
      <div class="card" v-for="film in films" :key="film.id">
        <img
          class="card-thumbnail"
          v-bind:src="film.image"
          v-bind:alt="film.title"
        />
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
      film: [],
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
      let film = this.films.find((movie) => movie.id == movieId);
      this.film.push(film);
      console.log(this.film[0]);
    },
    resetMovie() {
      this.film = [];
    },
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
  background: #e7fcff;
  font-family: monospace;
}

.modal {
  position: fixed;
  width: 300px;
  height: fit-content;
  padding:25px;
  background: #ffffff;
  box-shadow: 5px 5px 100px 10px #00000050;
  top: 25vh;
  z-index: 1000;
  left: calc(50vw - 150px);
  border-radius: 5px;
}

.modal-list {
  width: 90%;
  margin: 30px auto 0 auto;
  display: block;
  list-style-type: none;
}

.modal-close {
  background: #181826;
  color: #ffffff;
  font-size: 16px;
  margin: 30px auto 0 auto;
  padding: 0.7em 1.4em;
  border-radius: 50px;
  text-align: center;
  widows: fit-content;
  cursor: pointer;
}

.modal-close:hover {
  transition: .3s ease-in;
  background: #13e4e4;
}

.modal-title {
  font-size: 20px;
  color: #181826;
  text-align: center;
  font-weight: bold;
  border-bottom: 4px solid #13e4e4;
  width: 90%;
  margin: auto;
  padding-bottom: 10px;
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
  transition: 0.3s ease;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 5px 5px 10px 1px #00000020;
  z-index: 100;
  width: 64px;
  height: 64px;
  background: #13e4e4ea;
  color: #fff;
  font-size: 30px;
  font-weight: bold;
  border-radius: 50px;
  cursor: pointer;
  left: calc(50% - 32px);
  bottom: -32px;
}

.card-action:hover {
  transition: 0.3s ease;
  left: calc(50% - 75px);
  width: 150px;
  background: #13e4e4;
}

.card-thumbnail {
  width: 300px;
  border-radius: 5px;
  height: 450px;
}
</style>
