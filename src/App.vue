<template>
  <div class="container">

    <Header title="My Todo List"/>
    <AddTodo 
      @add-todo="
      addTodo"
    />
    
    <Todos 
      @delete-todo="deleteTodo" 
      @toggle-check="toggleCheck" 
      @on-enter="onBlur"
      :todos="todos"
    />

  </div>
</template>

<script>

import Header from './components/Header'
import Todos from './components/Todos'
import AddTodo from './components/AddTodo'


export default {
  name: 'App',
  components: {
    Header,
    Todos,
    AddTodo,

  },

  data() {
    return {
      todos: [],

    }
  },
  methods: {

    async addTodo(todo) {

      if (!this.todos.some(elem => elem.text === todo.text)) {
        
        const res = await fetch('api/todos/', {
          method: 'POST',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(todo)

        })

        const data = await res.json()

        this.todos = [...this.todos, data]

      } 
      
    },

    onBlur(id) {
      
      this.updateTodo(id)

    },

    async deleteTodo(id) {

      if (confirm('Are you sure ?')) {

        const res = await fetch(`api/todos/${id}`, {
          method: 'DELETE'
        })

        res.status === 200 ? (this.todos = this.todos.filter((todo) => todo.id !== id)) : alert('Error deleting todo')

      }
      
    },

    async updateTodo(id) {

      const elem = document.querySelectorAll('label')[id - 1].innerText
      const getTodo = await this.fetchTodo(id)
      const updateText = {...getTodo, text: elem}

      if (confirm('Are you sure you want to edit ?')) {

        const res = await fetch(`api/todos/${id}`, {
          method: 'PUT',
          headers: {
          'Content-type': 'application/json'
        },
          body: JSON.stringify(updateText)
        })

        const data = await res.json()

        this.todos = this.todos.map((todo) => 
          todo.id === id ? {...todo, text: data.text} : todo
        )

      }
      
    },

    async toggleCheck(id) {

      const checkToToggle = await this.fetchTodo(id)
      const updateCheck = {...checkToToggle, isDone: !checkToToggle.isDone}

      const res = await fetch(`api/todos/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updateCheck)
      })

      const data = await res.json()

      this.todos = this.todos.map((todo) => 
        todo.id === id ? {...todo, isDone: data.isDone} : todo
      )
    },

    async fetchTodos() {
      
      const res = await fetch('api/todos')
      const data = await res.json()

      return data
    },

    async fetchTodo(id) {

      const res = await fetch(`api/todos/${id}`)
      const data = res.json()

      return data

    }
  },

  async created() {
    this.todos = await this.fetchTodos()
  }


  
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;700&display=swap');

  *,
  *::before,
  *::after {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  body {
    background: #f4f4f4;
  }

  ul {
    list-style: none;
  }

  #app {
    font-family: 'Lato', sans-serif;
  }

  .container {
    width: 35%;
    margin-top: 2%;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid #ddd;
    padding: 20px 40px;
    background: #fff;
  }

</style>
