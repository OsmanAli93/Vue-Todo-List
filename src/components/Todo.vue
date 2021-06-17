<template>
    
    <input type="checkbox" @change="$emit('toggle-check', todo.id)" :id="todo.id" :value="todo.id" :checked="todo.isDone">

    <div class="wrapper">
        <div class="details">
            <label :data-id="todo.id" :class="[todo.isDone ? 'completed' : '']" :contenteditable="true" @keyup.enter="$emit('on-enter', todo.id)" title="Enter new text to update">
                {{ todo.text }}
            </label>
        </div>
        <div class="action">
            <i class="fas fa-times" @click="$emit('delete-todo', todo.id)"></i>
        </div>
    </div>
    
</template>

<script>

export default {
    name: 'Todo',
    props: {
        todo: Object
    },

}

</script>

<style scoped>
    .completed {
        text-decoration: line-through;
    }

    
    input[type="checkbox"] {
        margin-top: 10px;
        margin-right: 10px;
    }

    label {
        font-size: 14px;
        font-weight: bold;
        margin-bottom: 5px;
        display: block;
        padding: 6px 18px;
    }

    p {
        font-size: 14px;
    }

    .wrapper {
        display: flex;
        justify-content: space-between;
        flex: 1;
    }

    .far{
        color: #0d6efd;
        font-size: 18px;
        cursor: pointer;
        margin-right: 10px;
    }

    .fas {
        color: red;
        font-size: 18px;
        cursor: pointer;
    }
</style>
