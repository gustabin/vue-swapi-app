<!-- src/App.vue -->
<template>
  <div class="container mt-5">
    <div class="mb-4">
      <img src="./assets/logo.png" alt="star wars logo" class="logo">
      <h1>Star Wars Planets</h1>
    </div>
    <div class="form-group">
      <label for="sort">Sort by:</label>
      <select v-model="sortBy" id="sort" @change="sortData" class="form-control">
        <option value="name">Name</option>
        <option value="population">Population</option>
        <option value="diameter">Diameter</option>
        <!-- Add more options as needed -->
      </select>
    </div>
    <div v-for="planet in sortedPlanets" :key="planet.name" class="card mb-4">
      <div class="card-body">
        <h2 class="card-title">{{ planet.name }}</h2>
        <p class="card-text"><strong>Climate:</strong> {{ planet.climate }}</p>
        <p class="card-text"><strong>Diameter:</strong> {{ planet.diameter }}</p>
        <p class="card-text"><strong>Gravity:</strong> {{ planet.gravity }}</p>
        <p class="card-text"><strong>Population:</strong> {{ planet.population }}</p>
        <p class="card-text"><strong>Terrain:</strong> {{ planet.terrain }}</p>
        <!-- Add more information as needed -->
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'; // Import Axios

export default {
  data() {
    return {
      planets: [],
      sortBy: 'name',
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('https://swapi.dev/api/planets/');
        this.planets = response.data.results;
        this.sortData(); // Initial sorting
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
    sortData() {
      this.planets.sort((a, b) => {
        return a[this.sortBy].localeCompare(b[this.sortBy]);
      });
    },
  },
  computed: {
    sortedPlanets() {
      return [...this.planets]; // Create a copy to avoid mutating the original array
    },
  },
  watch: {
    sortBy() {
      this.sortData();
    },
  },
};
</script>

<style>
@import '~bootstrap/dist/css/bootstrap.css';

.container {
  max-width: 800px;
  margin: 0 auto;
}

.logo {
  max-width: 100%;
  height: auto;
  display: block;
  margin: 0 auto;
}
</style>
