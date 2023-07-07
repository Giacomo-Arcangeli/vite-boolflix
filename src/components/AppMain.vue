<script>
import ContentsCard from './ContentsCard.vue';
import { store } from '../data/store';
export default {
    components: { ContentsCard },
    data() {
        return {
            store,
        }
    }
};
</script>

<template>
    <!-- MOVIES -->
    <section id="movies">
        <h2>Movies</h2>
        <ContentsCard v-for="movie in store.movies" :key="movie.id" :item="movie" />
    </section>

    <!-- SERIES -->
    <section id="series">
        <h2>Series</h2>
        <ContentsCard v-for="serie in store.series" :key="serie.id" :item="serie" />
    </section>
</template>

<style lang="scss" scoped></style>
