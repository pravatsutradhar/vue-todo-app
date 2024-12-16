<template>
  <div>
    <ul>
      <li
          v-for="todo in todos"
          :key="todo.id"
          :class="{ completed: todo.completed }"
      >
        <input
            type="checkbox"
            :checked="todo.completed"
            @change="$emit('toggle-complete', todo.id)"
        />
        {{ todo.text }}
        <button @click="$emit('delete-todo', todo.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 8px 0;
}
.completed {
  text-decoration: line-through;
  color: gray;
}
button {
  padding: 4px 8px;
  background-color: red;
  color: white;
  border: none;
  cursor: pointer;
}
</style>
