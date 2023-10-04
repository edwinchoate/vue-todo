<template>
    <input v-bind:id="id" type="checkbox" v-bind:checked="isDone" />
    <label v-bind:for="id">{{ label }}</label>
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
    }
</script>
