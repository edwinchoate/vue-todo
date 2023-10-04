<template>
    <div>
        <input v-bind:id="id" type="checkbox" v-bind:checked="isDone" v-on:change="onChange" />
        <label v-bind:for="id">{{ label }}</label>
    </div>
</template>

<script>
    export default {
        name: 'TodoListItem',
        props: {
            label: { required: true, type: String },
            done: { default: false, type: Boolean },
            id: { required: true, type: String },
        },
        data() {
            return {
                isDone: this.done,
            };
        },
        methods: {
            onChange() {
                this.$emit('checkbox-changed');
            },
        }
    }
</script>

<style scoped>
    div {
        margin: 6px;
    }
    input {
        margin: 8px;
    }
</style>