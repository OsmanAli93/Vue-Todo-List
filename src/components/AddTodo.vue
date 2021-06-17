<template>
    <form @submit="onSubmit">
        <input type="text" v-model="text" name="todo" placeholder="What do you need to do today ?">
        <button type="submit">Add</button>
    </form>
</template>

<script>

export default {
    name: 'addTodo',
    data() {
        return {
            text: '',
            isDone: false
        }
    },
    methods: {
        onSubmit(event) {
            event.preventDefault()

            if (!this.text) {
                alert('Please add a todo')
                return
            }

            const newTodo = {
                // id: Math.floor(Math.random() * 100000),
                text: this.text,
                isDone: false,
                isEditable: true
            }

            this.$emit('add-todo', newTodo)

            this.text = ''

        } 
    }
}

</script>


<style scoped>
    form {
        display: flex;
        padding: 15px 0;
    }

    input {
        display: block;
        width: 100%;
        padding: 0.875rem 1.375rem;
        font-size: 1rem;
        line-height: 1;
        color: #495057;
        background-color: #fff;
        border: 1px solid #ced4da;
        border-radius: 2px;
        margin-right: 5px;
    }

    button {
       padding: 12px 24px;
       background-color: #0d6efd;
       border: 0;
       color: #fff;
       border-radius: 3px;
       cursor: pointer;
    }
</style>