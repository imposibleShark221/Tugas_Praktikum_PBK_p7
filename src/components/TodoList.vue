<!-- src/components/TodoList.vue -->
<template>
  <div class="todo-container">
    <h2>Todo List</h2>

    <form @submit.prevent="store.addTodo" class="form">
      <input
        v-model="store.newTodoText"
        placeholder="Tambah todo baru..."
        class="input"
      />
      <button type="submit" class="button">+</button>
    </form>

    <ul class="list">
      <li v-for="todo in store.todos" :key="todo.id" class="item">
        <label>
          <input type="checkbox" :checked="todo.done" @change="store.toggleTodo(todo.id)" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
        </label>
        <button @click="store.deleteTodo(todo.id)">x</button>
      </li>
    </ul>

    <div class="summary">
      <p>Selesai: {{ store.doneTodos }}</p>
      <p>Belum  : {{ store.unfinishedTodos.length }}</p>
      <p>Total  : {{ store.totalTodos }}</p>
    </div>
  </div>
</template>

<script setup>
import { useTodoStore } from '../stores/TodoStore'
const store = useTodoStore()
</script>

<style scoped>
.todo-container {
  background: #ffffff;
  padding: 2.5rem;
  border-radius: 16px;
  max-width: 600px;
  margin: auto;
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
  border: 1px solid #ddd;
  transition: box-shadow 0.3s ease;
}
.todo-container:hover {
  box-shadow: 0 12px 36px rgba(0,0,0,0.25);
}
.form {
  display: flex;
  gap: 12px;
  margin-bottom: 1.5rem;
}
.input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 1em;
  transition: border-color 0.3s ease;
}
.input:focus {
  border-color: #4a90e2;
  outline: none;
}
.button {
  padding: 1.5rem 1.5rem;
  background: #4a90e2;
  border: none;
  color: white;
  cursor: pointer;
  font-weight: 600;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(74, 144, 226, 0.4);
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}
.button:hover {
  background: #357ABD;
  box-shadow: 0 6px 12px rgba(53, 122, 189, 0.6);
}
.list {
  list-style: none;
  padding: 0;
  margin-top: 1rem;
}
.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;
  padding: 0.5rem 0.75rem;
  border-radius: 8px;
  border: 1px solid #ccc;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}
.item:hover {
  background-color: #f0f4ff;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}
.done {
  text-decoration: line-through;
  color: #999;
  font-style: italic;
}

button {
  background: #e74c3c;
  border: none;
  color: white;
  font-weight: bold;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  font-size: 16px;
  line-height: 1;
  transition: background-color 0.3s ease;
}
button:hover {
  background: #c0392b;
}

input[type="checkbox"] {
  accent-color: #27ae60;
  width: 18px;
  height: 18px;
  cursor: pointer;
}
.summary {
  margin-top: 1.5rem;
  font-weight: 700;
  color: #333;
  font-size: 1.1em;
}
</style>
