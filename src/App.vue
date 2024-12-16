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
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';

export default {
  components: { TodoInput, TodoList },
  data() {
    return {
      todos: [],
    };
  },
  computed: {
    remainingTasks() {
      return this.todos.filter(todo => !todo.completed).length;
    },
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({
        id: Date.now(),
        text: newTodo,
        completed: false,
      });
    },
    deleteTodo(todoId) {
      this.todos = this.todos.filter(todo => todo.id !== todoId);
    },
    toggleComplete(todoId) {
      const todo = this.todos.find(todo => todo.id === todoId);
      if (todo) todo.completed = !todo.completed;
    },
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
