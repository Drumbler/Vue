<template>
    <input v-model="newPoint">
    <button @click="save">
        Сохранить
    </button>
</template>

<script>
    export default {
        emits: ['add'], // эммитим метод add 
        data() {
            return { // дата возвращает пустой newPoint новой созданной заметки 
                newPoint: ''
            }
        },
        methods: {
            save() { // метод сохранения новой созданной заметки
                this.$emit('add', this.newPoint);
                this.newPoint = ''; 
            }
        }
    }
</script>

<style>

</style>