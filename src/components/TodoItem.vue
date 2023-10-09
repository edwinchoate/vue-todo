<template>
    <div v-if="!isEditing">
        <input v-bind:id="id" type="checkbox" v-bind:checked="isDone" v-on:change="onCheckboxChange" />
        <label v-bind:for="id">{{ label }}</label>
        <button v-on:click="onEditClick" ref="editButton" type="button">Edit</button>
        <button v-on:click="onDeleteClick" type="button">Delete</button>
    </div>
    <todo-item-edit-form v-else v-bind:old-label="label" v-bind:id="id" v-on:task-edit-save="saveEdit"
        v-on:task-edit-cancel="cancelEdit"></todo-item-edit-form>
</template>

<script>
    import TodoItemEditForm from './TodoItemEditForm.vue';

    export default {
        name: 'TodoItem',
        components: {
            TodoItemEditForm,
        },
        props: {
            label: { required: true, type: String },
            done: { default: false, type: Boolean },
            id: { required: true, type: String },
        },
        data() {
            return {
                isEditing: false,
            };
        },
        computed: {
            isDone() {
                return this.done;
            },
        },
        methods: {
            onCheckboxChange() {
                this.$emit('checkbox-changed');
            },
            onEditClick() {
                this.isEditing = true;
            },
            onDeleteClick() {
                this.$emit('task-deleted');
            },
            saveEdit(newLabel) {
                this.$emit('task-edit-save', newLabel);
                this.isEditing = false;
                this.focusOnEditBtn();
            },
            cancelEdit() {
                this.isEditing = false;
                this.focusOnEditBtn();
            },
            focusOnEditBtn() {
                this.$nextTick(() => {
                    const editBtn = this.$refs.editButton;
                    editBtn.focus();
                });
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
    button {
        margin-left: 12px;
    }
</style>