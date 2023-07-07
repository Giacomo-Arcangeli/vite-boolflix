<script>
import { poster } from '../data';
export default {
    props: {
        item: Object
    },
    computed: {
        hasFlag() {
            const availableFlags = ['it', 'en'];
            return availableFlags.includes(this.item.original_language);
        },
        flagSrc() {
            const url = new URL(`../assets/img/${this.item.original_language}.png`, import.meta.url);
            return url.href;
        },
        title() {
            return this.item.title || this.item.name;
        },
        originalTitle() {
            return this.item.original_title || this.item.original_name;
        },
        posterPath() {
            if (!this.item.poster_path) return poster.placeholder;
            return poster.prefix + this.item.poster_path;
        },
        vote() {
            return Math.ceil(this.item.vote_average / 2);
        }
    },
    methods: {
        StarType(n) {
            return n <= this.vote ? 'fas' : 'far';
        }
    }
};
</script>


<template>
    <ul>
        <li>{{ title }}</li>
        <li>{{ originalTitle }}</li>
        <li>
            <img v-if="hasFlag" :src="flagSrc" alt="">
            <span v-else>{{ item.original_language }}</span>
        </li>
        <li><i v-for="n in 5" :key="n" :class="StarType(n)" class="fa-star"></i></li>
        <li><img :src="posterPath" alt=""></li>
    </ul>
</template>


<style lang="scss" scoped>
ul {
    margin: 20px 0;
    border-top: 2px solid black;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
</style>