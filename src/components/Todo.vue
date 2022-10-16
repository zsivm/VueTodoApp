<template>
  
  <div class="todo-row">
    <div class="todo-cont" v-if="!editMode">
      <div class="todo-elements">
        <p :class="{ 'completed': todo.completed }" @click="markComplete">{{ todo.title }}</p>
        <div>
          <button @click="editMode = true">Edit</button>
          <button @click="$emit('delete-todo', todo.id)">X</button>
        </div>
      </div>
      <p class="timeStamp">{{ todo.timeStamp }}</p>
    </div>
    <div class="todo-cont" v-else>
      <div class="todo-elements">
        <input type="text" v-model="todo.title">
        <div>
          <button @click="editMode = false">Ok</button>
          <button @click="onCancleClicked">Cancel</button>
        </div>
      </div>
      <p class="timeStamp">{{ todo.timeStamp }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
   data() {
      return {
        editMode: false,
        oldTitle: this.todo.title
      }
    },
  props: [
    "todo"
  ],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
      this.$emit("todo-clicked");
    },
    onCancleClicked() {
      this.todo.title = this.oldTitle;
      this.editMode = false;
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
    margin-top: 10px;
    background-color: #eee;
    border-radius: 10px;
  }
  .todo-elements {
    display: flex;
    justify-content: space-between;
  }
  .todo-cont {
    padding-bottom: 10px;
  }
  .timeStamp {
    margin-top: 0px;
    margin-bottom: 0px;
    font-size: 12px;
  }
  p {
    margin-left: 10px;
    font-family: arial;
    font-size: 18px;
  }
  input {
    width: 50%;
    height: 2em;
    margin: auto 0;
    margin-left: 10px;
    font-size: 18px;
  }
  button {
    width: 35px;
    height: 35px;
    margin: 10px;
    border-radius: 10px;
    background-color: #fff;
  }
</style>