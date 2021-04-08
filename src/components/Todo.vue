<template>
  <div class="todo-row">
    <p v-bind:class="{ 'completed': todo.completed }" @click="markComplete">{{ todo.title }}</p>
    <button @click="$emit('delete-todo', todo.id)">X</button>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: [
    "todo"
  ],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
}
</script>

<style scoped>
  .completed {
    text-decoration: line-through;
    text-decoration-color: red;
  }
  .todo-row {
    display: flex;
    justify-content: space-between;
    background-color: #eee;
    border: 1px solid black;
    border-radius: 10px 0 10px 0;
    margin-top: 10px;
  }
  p {
    margin-left: 10px;
    font-size: 18px;
  }
  button {
    width: 35px;
    height: 35px;
    margin: 10px;
  }
</style>