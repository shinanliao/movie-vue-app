<template>
  <div class="movies-index">
    <h1>My Movies</h1>
    <br />
    Search:
    <input placeholder="Search by Title" v-model="titleFilter" />
    <div class="row">
      <div class="col-sm-4" v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">{{ movie.year }}</p>
            <p>{{ movie.plot }}</p>
            <router-link class="btn btn-info" :to="`/movies/${movie.id}`">Movie Details</router-link>
          </div>
        </div>
      </div>
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
