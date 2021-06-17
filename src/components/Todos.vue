<template>
    <ul id="todo-list">
        <li :key="todo.id" v-for="(todo, index) in todos" :class="[index === todos.length - 1 ? 'last-child' : '']">
            <Todo :todo="todo" 
                @delete-todo="$emit('delete-todo', todo.id)" 
                @toggle-check="$emit('toggle-check', todo.id)" 
                @update-todo="$emit('update-todo', todo.id)"
                @on-enter="$emit('on-enter', todo.id)"
            />
        </li>
    </ul>
</template>

<script>

import Todo from './Todo'

export default{
    name: 'Todos',
    props: {
        todos: Array
    },
    components: {
        Todo
    },
    emits: ['delete-todo', 'toggle-check', 'update-todo', 'on-enter']
}
</script>

<style scoped>

    ul li {
        padding: 20px 0;
        border-bottom: 1px solid #ccc;
        display: flex;
        
    }

    .last-child {
        border-bottom: 0;
    }
    
</style>
