<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <AddTodo 
      @add-todo="addTodo"
    />
    <select v-model="filter">
        <option value="all">ALL</option>
        <option value="completed">COMPLETED</option>
        <option value="not-completed">NOT COMPLETED</option>
    </select>
    <hr>
    <Loader v-if="loading"/>
    <TodoList 
      v-else-if='filteredTodos.length'
      v-bind:filteredTodos='todos'
      @remove-filteredTodos="removeTodo"
    />
    <p v-else>Nothing to do!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },

  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        this.todos=json
        this.loading = false
      })
  },

  computed: {
      filteredTodos() {
          if (this.filter === 'all') {
              return this.todos
          }

          if (this.filter === 'comleted') {
              return this.todos.filter(todo => todo.completed = true)
          }

          if (this.filter === 'not-completed') {
              return this.todos.filter(todo => todo.completed = false)
          }
          
      }
  },

  components: {
    TodoList,
    AddTodo,
    Loader
  },

  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  }
}
</script>