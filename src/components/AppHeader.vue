<script>
import SearchForm from "./SearchForm.vue";

export default {
    components: { SearchForm },
    data() {
        return {

        };
    },
    emits: ['search-movie'],
    methods: {
        setTitleFilter(term) {
            this.$emit('search-movie', term)
        },
    },
};
</script>

<template>
    <SearchForm @term-change="setTitleFilter" />
</template>

<style></style>
