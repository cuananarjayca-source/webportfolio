<script setup>
import { computed, onMounted, ref } from 'vue'

const navOpen = ref(false)
const theme = ref('dark')

const toggleNav = () => {
  navOpen.value = !navOpen.value
}

const closeNav = () => {
  navOpen.value = false
}

const setThemeClass = (mode) => {
  document.body.classList.toggle('light-theme', mode === 'light')
  document.body.classList.toggle('dark-theme', mode === 'dark')
}

const toggleTheme = () => {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
  setThemeClass(theme.value)
  localStorage.setItem('portfolio-theme', theme.value)
}

const themeClass = computed(() => (theme.value === 'dark' ? 'navbar-dark bg-dark' : 'navbar-light bg-white'))
const linkClass = computed(() => (theme.value === 'dark' ? 'text-white' : 'text-dark'))
const buttonVariant = computed(() => (theme.value === 'dark' ? 'btn-outline-light' : 'btn-outline-dark'))
const themeLabel = computed(() => (theme.value === 'dark' ? 'Light mode' : 'Dark mode'))

onMounted(() => {
  const storedTheme = localStorage.getItem('portfolio-theme')
  if (storedTheme === 'light' || storedTheme === 'dark') {
    theme.value = storedTheme
  }
  setThemeClass(theme.value)
})
</script>

<template>
  <nav :class="['navbar', 'navbar-expand-lg', 'fixed-top', themeClass]" id="navBar">
    <div class="container-fluid position-relative">
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
          <a class="nav-link" :class="linkClass" href="#landing" @click="closeNav">Home</a>
          <a class="nav-link" :class="linkClass" href="#projects" @click="closeNav">My Projects</a>
          <a class="nav-link" :class="linkClass" href="#tools" @click="closeNav">Tools</a>
          <a class="nav-link" :class="linkClass" href="#contact" @click="closeNav">Contacts</a>
        </div>
      </div>

      <button
        type="button"
        class="btn theme-toggle-btn"
        :class="buttonVariant"
        @click="toggleTheme"
        aria-label="Toggle theme"
      >
        {{ themeLabel }}
      </button>
    </div>
  </nav>
</template>

