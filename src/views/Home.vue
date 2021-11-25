<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="score in scores" v-bind:key="score.id">
    <p>School Name: {{ score.school_name }}</p>
    <p>SAT Math: {{ score.sat_math_avg_score }}</p>
    <p>SAT Reading: {{ score.sat_critical_reading_avg_score }}</p>
    <br>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        scores: {},
      };
    },
    created: function () {
      this.getScores()
    },
    methods: {
      getScores: function() {
        axios.get('https://data.cityofnewyork.us/resource/f9bf-2cp4.json').then(response => {
          this.scores = response.data;
        });
      }
    },
  };
</script>
