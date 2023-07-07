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
        <li>{{ item.vote_average }}</li>
        <li><img :src="posterPath" alt=""></li>
    </ul>
</template>


<style lang="scss" scoped></style>