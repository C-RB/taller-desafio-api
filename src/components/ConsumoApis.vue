<template>
    <div>
     <h2>Consumo de API </h2>
  
      <button @click="getPopulation">obtencion de  Population Data</button>
      <button @click="getAnimeRecommendations">obtencion de  Anime Recommendations</button>
      <button @click="getRandomAnime">obtencion de  Random Anime</button>
      <button @click="getRandomManga">obtencion de  Random Manga</button>


  
      <div v-if="population.length">
        <h2>Country Population</h2>
        <ul>
          <li v-for="country in population" :key="country.country">
            {{ country.country }} - Population: {{ country.populationCounts[0].value }}
          </li>
        </ul>
      </div>
  
      <div v-if="animeRecommendations.length">
        <h2>Anime Recommendations</h2>
        <ul>
          <li v-for="anime in animeRecommendations" :key="anime.entry.mal_id">
            {{ anime.entry.title }}
          </li>
        </ul>
      </div>
  
      <div v-if="randomAnime">
        <h2>Random Anime</h2>
        <p>{{ randomAnime.title }} - {{ randomAnime.synopsis }}</p>
      </div>
  
      <div v-if="randomManga">
        <h2>Random Manga</h2>
        <p>{{ randomManga.title }} - {{ randomManga.synopsis }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        population: [],
        animeRecommendations: [],
        randomAnime: null,
        randomManga: null
      };
    },

// METODOS PARA EL CONSUMO 
    methods: {
      async getPopulation() {
        try {
          const response = await axios.get('https://countriesnow.space/api/v0.1/countries/population');
          this.population = response.data.data;
        } catch (error) {
          console.error('Error fetching country population:', error);
        }
      },
      async getAnimeRecommendations() {
        try {
          const response = await axios.get('https://api.jikan.moe/v4/recommendations/anime');
          this.animeRecommendations = response.data.data;
        } catch (error) {
          console.error('Error fetching anime recommendations:', error);
        }
      },
      async getRandomAnime() {
        try {
          const response = await axios.get('https://api.jikan.moe/v4/random/anime');
          this.randomAnime = response.data.data;
        } catch (error) {
          console.error('Error fetching random anime:', error);
        }
      },
      async getRandomManga() {
        try {
          const response = await axios.get('https://api.jikan.moe/v4/random/manga');
          this.randomManga = response.data.data;
        } catch (error) {
          console.error('Error fetching random manga:', error);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  button {
    background-color: #720d0d;
    color: white;
    padding: 10px;
    
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin: 5px 0;
  }
  </style>
  