<script setup>
import { ref } from 'vue'

const navOpen = ref(false)

const toggleNav = () => {
  navOpen.value = !navOpen.value
}

const closeNav = () => {
  navOpen.value = false
}
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top" id="navBar">
    <div class="container-fluid">
      <button
        class="navbar-toggler"
        type="button"
        @click="toggleNav"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="navbar-collapse" :class="{ collapse: !navOpen, show: navOpen }" id="navbarNavAltMarkup">
        <div class="navbar-nav mx-auto">
          <a class="nav-link text-white" href="#landing" @click="closeNav">Home</a>
          <a class="nav-link text-white" href="#projects" @click="closeNav">My Projects</a>
          <a class="nav-link text-white" href="#tools" @click="closeNav">Tools</a>
          <a class="nav-link text-white" href="#contact" @click="closeNav">Contacts</a>
        </div>
      </div>
    </div>
  </nav>
</template>


