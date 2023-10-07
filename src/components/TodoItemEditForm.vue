<template>
    <form v-on:submit.prevent="onSubmit">
        <input type="text" autocomplete="off" ref="labelInput" v-model.trim="newLabel" />
        <button type="submit">✔</button>
        <button type="button" v-on:click="onCancel">✖</button>
    </form>
</template>

<script>
    export default {
        name: 'TodoItemEditForm',
        props: {
            oldLabel: { required: true, type: String },
            id: { required: true, type: String },
        },
        data() {
            return {    
                newLabel: this.oldLabel,
            }
        },
        mounted() {
            const labelInput = this.$refs.labelInput;
            labelInput.focus();
            labelInput.select();
        },
        methods: {
            onSubmit() {
                this.$emit('task-edit-save', this.newLabel);
            },
            onCancel() {
                this.$emit('task-edit-cancel');
            },
        }
    };
</script>