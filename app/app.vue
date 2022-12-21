<template>
  <div class="cols d-flex">
    <div class="col">
      <BaseDisplay />
    </div>

    <div class="col">
      <PhotoGallery />
    </div>
  </div>
</template>

<script setup>
import BaseDisplay from './components/BaseDisplay';
import PhotoGallery from './components/PhotoGallery';
</script>

<style>
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
