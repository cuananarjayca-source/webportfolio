<script setup>
const props = defineProps({
  project: Object
})
</script>

<template>
  <div class="card w-100">
    <img :src="props.project.image" class="card-img-top card-img" alt="Project image" />
    <div class="card-body">
      <h5 class="card-title">{{ props.project.title }}</h5>
      <p class="card-text">{{ props.project.description }}</p>
    </div>
  </div>
</template>

<style scoped>
</style>