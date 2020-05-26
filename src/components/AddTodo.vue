<template>
    <form @submit.prevent="onSubmit">
        <input tupe="text" v-model="title">
        <button type="submit">Create Todo</button>
    </form>
</template>

<script>
export default {
    
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    completed: false
                }
                this.$emit('add-todo', newTodo)
                this.title = ''
            }
        }
    }
}

</script>

<style scoped>
    form {
        display: flex;
    }

    input {
        width: 60rem;
    }
</style>