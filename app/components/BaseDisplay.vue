<template>
  <img src="/todo.jpg" alt="todo photo by Glenn Carstens Peters" width="150" />
  <p>
    Photo by
    <a
      href="https://unsplash.com/@glenncarstenspeters?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText"
      >Glenn Carstens-Peters</a
    >
    on
    <a
      href="https://unsplash.com/s/photos/todo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText"
      >Unsplash</a
    >
  </p>
  <button @click="fetchTodoList">Fetch Data</button>

  <ul>
    <li v-for="todo in todoList" :key="`todo-id-${todo.id}`">
      <input type="checkbox" v-model="todo.completed" />
      {{ todo.title }}
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue';
const todoList = ref([]);

const fetchTodoList = () => {
  fetch('https://jsonplaceholder.typicode.com/todos')
    .then((response) => response.json())
    .then((json) => {
      todoList.value = json;
    });
};
</script>
