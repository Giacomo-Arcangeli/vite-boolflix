<script>
import { api } from './data';
import { store } from './data/store';
import AppHeader from './components/AppHeader.vue';
import axios from 'axios';
import ContentsCard from './components/ContentsCard.vue';


// *********************
export default {
  components: { AppHeader, ContentsCard },
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
    <ContentsCard v-for="movie in store.movies" :key="movie.id" />

  </section>

  <!-- SERIES -->
  <section id="series">
    <h2>Series</h2>
    <ContentsCard v-for="serie in store.series" :key="serie.id" />
  </section>
</template>

<style lang="scss"></style>
