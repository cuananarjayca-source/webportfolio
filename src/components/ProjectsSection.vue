<script setup>
import { computed } from 'vue'
import ProjectCard from './ProjectCard.vue'
import projects from '../data/projects.json'

const chunkSize = 3

const chunkedProjects = computed(() => {
  const chunks = []
  for (let i = 0; i < projects.length; i += chunkSize) {
    chunks.push(projects.slice(i, i + chunkSize))
  }
  return chunks
})
</script>

<template>
  <section class="pb-5" id="projects">
    <h1 class="mt-5 mb-5 pb-4 text-center">My Projects</h1>
    <div
      v-for="(group, index) in chunkedProjects"
      :key="index"
      class="row my-5 justify-content-center gx-3"
    >
      <div v-for="project in group" :key="project.id" class="col-12 col-sm-6 col-md-4 col-lg-3 mb-4 d-flex">
        <ProjectCard :project="project" />
      </div>
    </div>
  </section>
</template>