<script>
import { api } from './data';
import { store } from './data/store';
import AppHeader from './components/AppHeader.vue';
import axios from 'axios';


// *********************
export default {
  components: { AppHeader },
  data() {
    return {
      titleFilter: '',
      store
    }
  },
  methods: {
    changeTitleFilter(term) {
      console.log('changeTitleFilter', term)
      this.titleFilter = term;
      this.searchContents()
    },
    searchContents() {
      if (!this.titleFilter) {
        store.movies = [];
        store.series = [];
        return;
      };

      const { baseUri, key, language } = api;

      // chiamata per i movies
      axios.get(`${baseUri}/search/movie?api_key=${key}&language=${language}&query=${this.titleFilter}`)
        .then((res) => {
          store.movies = res.data.results;
        })

      // chiamata per le series
      axios.get(`${baseUri}/search/tv?api_key=${key}&language=${language}&query=${this.titleFilter}`)
        .then((res) => {
          store.series = res.data.results;
        })
    }
  }

};
</script>

<template>
  <AppHeader @search-movie="changeTitleFilter" />

  <!-- MOVIES -->
  <section id="movies">
    <h2>Movies</h2>
    <ul v-for="movie in store.movies" :key="movie.id">
      <li>{{ movie.title }}</li>
      <li>{{ movie.original_title }}</li>
      <li>{{ movie.original_language }}</li>
      <li>{{ movie.vote_average }}</li>
    </ul>
  </section>

  <!-- SERIES -->
  <section id="series">
    <h2>Series</h2>
    <ul v-for="serie in store.series" :key="serie.id">
      <li>{{ serie.name }}</li>
      <li>{{ serie.original_name }}</li>
      <li>{{ serie.original_language }}</li>
      <li>{{ serie.vote_average }}</li>
    </ul>
  </section>
</template>

<style lang="scss"></style>
