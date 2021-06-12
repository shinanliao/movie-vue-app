<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h3>Title: {{ movie.title }}</h3>
      <p>Plot: {{ movie.plot }}</p>
      <p>Year: {{ movie.year }}</p>
      <router-link :to="`/movies/${movie.id}`">More Information</router-link>
      <br />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log("Movies array", response.data);
      this.movies = response.data;
    });
  },
};
</script>
