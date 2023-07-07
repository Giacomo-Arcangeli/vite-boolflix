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
    <main>
        <div class="container">
            <!-- MOVIES -->
            <section id="movies">
                <h2 class="mt-3">Movies</h2>
                <div class="movie-section">
                    <ContentsCard v-for="movie in store.movies" :key="movie.id" :item="movie" />
                </div>
            </section>

            <!-- SERIES -->
            <section id="series">
                <h2 class="mt-3">Series</h2>
                <ContentsCard v-for="serie in store.series" :key="serie.id" :item="serie" />
            </section>
        </div>
    </main>
</template>


<style lang="scss" scoped>
main {
    height: calc(100vh - 100px);
    background-color: grey;
    overflow: auto;
}
</style>
