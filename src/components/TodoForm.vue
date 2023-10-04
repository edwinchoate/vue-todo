<template>
    <form v-on:submit.prevent="onSubmit" >
        <input id="new-todo-input" type="text" name="new-todo-input" autocomplete="off" v-model.trim="inputText" />
        <button type="submit">Add task</button>
    </form>
</template>

<script>
    export default {
        name: 'TodoForm',
        data() {
            return {
                inputText: '',
            };
        },
        methods: {
            onSubmit() {
                if (this.inputText === '') return;
                this.$emit('task-created', this.inputText);
                this.inputText = '';
            }
        }
    }
</script>
