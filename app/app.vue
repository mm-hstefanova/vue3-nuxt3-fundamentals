<template>
  <div class="cols d-flex">
    <div class="col">
      <img
        src="/todo.jpg"
        alt="todo photo by Glenn Carstens Peters"
        width="150"
      />
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
    </div>

    <div class="col">
      <button @click="fetchImages">Fetch Images</button>
      <span
        >Number of photos: {{ numberOfPhotos }} / {{ evenAlbums }} Event
        Albums</span
      >
      <div class="d-flex">
        <div v-for="img in images" :key="`img-id-${img.id}`">
          <img :src="img.thumbnailUrl" :alt="img.title" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const todoList = ref([]);
const images = ref([]);

const numberOfPhotos = computed(() => todoList.value?.length);
const evenAlbums = computed(
  () => images.value?.filter((img) => img.albumId % 2 === 0).length
);

const fetchTodoList = () => {
  fetch('https://jsonplaceholder.typicode.com/todos')
    .then((response) => response.json())
    .then((json) => {
      todoList.value = json;
    });
};

const fetchImages = () => {
  fetch('https://jsonplaceholder.typicode.com/photos')
    .then((response) => response.json())
    .then((json) => (images.value = json));
};
</script>

<style scoped>
.col {
  flex-basis: 50%;
}

.d-flex {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-wrap: wrap;
}
</style>
