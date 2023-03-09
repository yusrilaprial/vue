<template>
    <button class="btn btn-primary" @click="changeText">Ubah Header</button>
    <h2>{{ text }}</h2>
</template>

<script>
export default {
    name: 'HeaderWeb',
    props: ["text"],
    data() {
        return {
            newText: "Ini adalah header dari HeaderWeb.vue",
        }
    },
    methods: {
        changeText() {
            this.$emit("changeTitle", this.newText);
        },
    },
    emits: ["changeTitle"],
}
</script>

<style>

</style>