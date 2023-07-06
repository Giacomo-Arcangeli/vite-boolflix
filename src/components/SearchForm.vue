<script>
export default {
    data() {
        return {
            searchTerm: ''
        }
    },
    emits: ['term-change']
}
</script>



<template>
    <form @submit.prevent="$emit('term-change', searchTerm)">
        <input type="text" placeholder="Scrivi qui..." v-model.trim="searchTerm">
        <button>Cerca</button>
    </form>
</template>



<style></style>