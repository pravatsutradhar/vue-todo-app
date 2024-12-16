<template>
    <div>
      <input
        v-model="todoText"
        type="text"
        placeholder="Enter a task"
        @keyup.enter="submitTodo"
      />
      <button @click="submitTodo">Add</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        todoText: '',
      };
    },
    methods: {
      submitTodo() {
        if (this.todoText.trim()) {
          this.$emit('add-todo', this.todoText);
          this.todoText = '';
        }
      },
    },
  };
  </script>
  
  <style scoped>
  input {
    padding: 8px;
    margin-right: 8px;
    width: 70%;
  }
  button {
    padding: 8px 16px;
  }
  </style>
  