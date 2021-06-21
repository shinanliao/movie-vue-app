<template>
  <div class="home">
    <h1 style="font-family: georgia">{{ message }}</h1>
    <img src="/../../cinema.jpg" alt="Cinema" style="border: 4px solid black" />
  </div>
</template>

<style></style>

<script>
// import axios from "axios";
export default {
  data: function () {
    return {
      message: "My Favorite Movies",
    };
  },
  created: function () {},
  methods: {},
};
</script>
