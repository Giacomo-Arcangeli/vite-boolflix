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
    <form @submit.prevent="$emit('term-change', searchTerm)" class="">
        <input class="form-control" type="text" placeholder="Scrivi qui..." v-model.trim="searchTerm">
        <button class="btn ms-2">Cerca</button>
    </form>
</template>



<style lang="scss" scoped>
form {
    display: flex;
}

button {
    background-color: red;
    color: white;
}
</style>