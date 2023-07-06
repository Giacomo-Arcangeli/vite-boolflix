<script>
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
        }
    }
};
</script>


<template>
    <ul>
        <li>{{ item.title || item.name }}</li>
        <li>{{ item.original_title || item.original_name }}</li>
        <li>
            <img v-if="hasFlag" :src="flagSrc" alt="">
            <span v-else>{{ item.original_language }}</span>
        </li>
        <li>{{ item.vote_average }}</li>
    </ul>
</template>


<style lang="scss" scoped></style>