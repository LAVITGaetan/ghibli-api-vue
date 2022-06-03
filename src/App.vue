<template>
  <div id="app">
    <h1>Ghibli API</h1>
    <ul v-if="films.length > 0">
    <li v-for="film in films" :key="film.id">{{ film.title }}</li>
  </ul>
    
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_uri: "https://ghibliapi.herokuapp.com/films",
      films : {}
    };
  },
  methods : {
    fetchApi() {
      fetch(this.api_uri)
      .then(res => {
        return res.json();
      })
      .then(data => {
        this.films = data;
    })
    }
  },
  beforeMount() {
    this.fetchApi()
  }
};
</script>

<style></style>
