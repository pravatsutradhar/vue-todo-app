<template>
  <div id="app" class="todo-app">
    <h1>Todo App</h1>
    <TodoInput @add-todo="addTodo" />
    <TodoList
        :todos="todos"
        @delete-todo="deleteTodo"
        @toggle-complete="toggleComplete"
    />
    <p>Total tasks: {{ todos.length }}</p>
    <p>Remaining tasks: {{ remainingTasks }}</p>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';

export default {
  components: { TodoInput, TodoList },
  setup() {
    const todos = ref([]);

    const addTodo = (newTodo) => {
      todos.value.push({
        id: Date.now(),
        text: newTodo,
        completed: false,
      });
    };

    const deleteTodo = (todoId) => {
      todos.value = todos.value.filter(todo => todo.id !== todoId);
    };

    const toggleComplete = (todoId) => {
      const todo = todos.value.find(todo => todo.id === todoId);
      if (todo) {
        todo.completed = !todo.completed;
      }
    };

    const remainingTasks = computed(() => {
      return todos.value.filter(todo => !todo.completed).length;
    });

    return {
      todos,
      addTodo,
      deleteTodo,
      toggleComplete,
      remainingTasks,
    };
  },
};
</script>

<style>
.todo-app {
  font-family: Arial, sans-serif;
  text-align: center;
  max-width: 500px;
  margin: 0 auto;
}
</style>
