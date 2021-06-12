<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <p>{{ movie.plot }}</p>
    <p>{{ movie.year }}</p>
    <p>{{ movie.genre }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
    <br />
    <button v-on:click="destroyMovie()">Delete Movie</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log("Post object", response.data);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function () {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
