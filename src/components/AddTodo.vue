<template>
  <div class="form-wrapper">
    <form @submit="addTodo">
      <input placeholder="Do something..." type="text" v-model="title" name="title">
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';

export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo(e) {
      e.preventDefault();

      const newTodoObj = {
        id: uuidv4(),
        title: this.title,
        completed: false
      }

      this.$emit('add-todo', newTodoObj);
      this.title = '';
    }
  }
}
</script>

<style scoped>
.form-wrapper {
  display: flex;
  justify-content: center;
}
input {
  box-shadow: 2px 2px rgba(0, 0, 0, 0.25);
  font-size: 15px;
  width: 250px;
  height: 40px;
  padding-left: 8px;
  border-radius: 10px;
  margin-right: 20px;
}
button {
  box-shadow: 2px 2px rgba(0, 0, 0, 0.25);
  border-radius: 4px;
  height: 35px;
}
</style>