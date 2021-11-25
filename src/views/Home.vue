<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
    <button v-on:click="setSortAttribute('school_name')">Sort by School</button>
        Search: <input type="text" v-model="searchTerm" list="school_names">
        <datalist id="school_names">
          <option v-for="score in scores">{{ score.school_name }}</option>
        </datalist>
          <div v-for="score in filterBy(scores, searchTerm, 'school_name')">
            <div v-for="post in orderBy(scores, sortAttribute, sortOrder)">
            </div>
          </div>
    </div>
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
import Vue2Filters from 'vue2-filters';

  export default {
    mixins: [Vue2Filters.mixin],
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        scores: {},
        searchTerm: "",
        sortAttribute: 'school_name',
        sortOrder: 1
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
      },
      setSortAttribute: function(attribute) {
        this.sortAttribute = attribute;
      },
    },
  };
</script>
