<template>
  <div id="app">
    <h2>My todolist</h2>
    <AddTodo @add-todo="addTodo"/>
    <Todos :todos="todos" @delete-todo="deleteTodo" @todo-clicked="saveTodos"/>
  </div>
</template>

<script>
  import Todos from './components/Todos.vue';
  import AddTodo from './components/AddTodo.vue';

  export default {
    name: 'app',
    components: {
      Todos,
      AddTodo
    },
    data() {
      return {
        todos: []
      }
    },
    mounted() {
      if(localStorage.getItem('todos')) {
        try {
          this.todos = JSON.parse(localStorage.getItem('todos'));
        } catch(e) {
          localStorage.removeItem('todos');
        }
      }
    },
    methods: {
      addTodo(newTodo) {
        if(newTodo.title) {
          this.todos.push(newTodo);
          this.saveTodos();
        }
      },
      deleteTodo(todoId) {
        this.todos = this.todos.filter(todo => todo.id != todoId);
        this.saveTodos();
      },
      saveTodos() {
        const parsed = JSON.stringify(this.todos);
        localStorage.setItem('todos', parsed);
      }
    }
  }
</script>

<style scoped>
  #app {
    margin: auto;
    width: 50%;
  }
  h2 {
    text-align: center;
  }
</style>