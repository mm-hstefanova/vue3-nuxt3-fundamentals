<template>
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
</template>

<script setup>
import { ref, computed } from 'vue';

const images = ref([]);

const fetchImages = () => {
  fetch('https://jsonplaceholder.typicode.com/photos')
    .then((response) => response.json())
    .then((json) => (images.value = json));
};

const numberOfPhotos = computed(() => todoList.value?.length);
const evenAlbums = computed(
  () => images.value?.filter((img) => img.albumId % 2 === 0).length
);
</script>
