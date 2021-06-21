<template>
  <div class="movies-index">
    <input type="text" v-model="titleFilter" placeholder="Search" />
    <div v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
      <h3 style="color: black">Title: {{ movie.title }}</h3>
      <p style="color: gray">Plot: {{ movie.plot }}</p>
      <p>Year: {{ movie.year }}</p>
      <router-link :to="`/movies/${movie.id}`">More Information</router-link>
      <br />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
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
