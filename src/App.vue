<script>
import { api } from './data';
import { store } from './data/store';
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';


// *********************
export default {
  components: { AppHeader, AppMain },
  data() {
    return {
      titleFilter: '',
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
  <AppMain />
</template>

<style lang="scss"></style>
