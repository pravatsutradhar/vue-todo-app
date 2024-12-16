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
import {ref} from 'vue';

export default {
  emits: ['add-todo'],
  setup(props, {emit}) {
    const todoText = ref('');

    const submitTodo = () => {
      if (todoText.value.trim()) {
        emit('add-todo', todoText.value);
        todoText.value = '';
      }
    };

    return {
      todoText,
      submitTodo,
    };
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
