<template>
  <div class="home">
    <h1>Shinan's Favorite Movies</h1>
    Title:
    <input type="text" v-model="newMovieTitle" />
    <br />
    Plot:
    <input type="text" v-model="newMoviePlot" />
    <br />
    Year:
    <input type="text" v-model="newMovieYear" />
    <br />
    Genre:
    <input type="text" v-model="newMovieGenre" />
    <br />
    <button v-on:click="createMovie()">Create Movie</button>

    <div v-for="movie in movies" v-bind:key="movie.id">
      <h3>Title: {{ movie.title }}</h3>
      <button v-on:click="showMovie(movie)">More Info</button>
      <p>Plot: {{ movie.plot }}</p>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info</h1>
        <p>Title: ...</p>
        <p>Plot: ...</p>
        <p>Year: ...</p>
        <p>Genre: ...</p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newMovieTitle: "",
      newMoviePlot: "",
      newMovieYear: "",
      newMovieGenre: "",
    };
  },
  created: function () {
    this.indexMovies();
  },

  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = {
        title: this.newMovieTitle,
        plot: this.newMoviePlot,
        year: this.newMovieYear,
        genre: this.newMovieGenre,
      };
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          console.log("Success!", response.data);
          this.movies.unshift(response.data);
          this.newMovieTitle = "";
          this.newMoviePlot = "";
          this.newMovieYear = "";
          this.newMovieGenre = "";
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
    showMovie: function (movie) {
      console.log(movie);
      document.querySelector("#movie-details").showModal();
    },
  },
};
</script>
