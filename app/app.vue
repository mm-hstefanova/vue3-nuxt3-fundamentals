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

<script>
import { defineNuxtComponent } from '#app';

export default defineNuxtComponent({
  data: () => ({
    todoList: [],
    images: [],
  }),
  computed: {
    numberOfPhotos() {
      return this.images?.length;
    },
    evenAlbums() {
      return this.images.filter((img) => img.albumId % 2 === 0).length;
    },
  },
  methods: {
    fetchTodoList() {
      fetch('https://jsonplaceholder.typicode.com/todos')
        .then((response) => response.json())
        .then((json) => {
          this.todoList = json;
        });
    },
    fetchImages() {
      fetch('https://jsonplaceholder.typicode.com/photos')
        .then((response) => response.json())
        .then((json) => (this.images = json));
    },
  },
});
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
