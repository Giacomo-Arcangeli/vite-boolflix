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
    <header class="bg-black">
        <div class="container">
            <h1>BOOLFLIX</h1>
            <SearchForm @term-change="setTitleFilter" />
        </div>
    </header>
</template>

<style lang="scss" scoped>
.container {
    height: 100px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

h1 {
    color: red;
}
</style>
