<script setup>
const name = 'Arjay'
const tagline = "I'm an aspiring Full Stack Web Developer"
const bio = `Junior Full-Stack Developer with a background in IT operations and technical support. Recently completed intensive web development training focused on JavaScript, Vue, Node.js, MongoDB, and REST APIs. Experienced in problem-solving, system analysis, and AI-assisted learning. Seeking to contribute to modern web application development while continuing to grow as a software engineer.`
const profileImage = 'images/profile.png'
</script>

<template>
  <section id="landing" class="container-fluid py-5 text-light px-0">
    <div class="row justify-content-center">
      <div class="col-12 col-lg-10 col-xl-8 text-center">
        <h1>Hi! I am {{ name }}</h1>
        <h2>{{ tagline }}</h2>
        <p class="mx-auto">{{ bio }}</p>
        <div class="mt-4 mb-4">
          <a href="#contact" class="btn btn-hire">Hire Me</a>
        </div>
        <div class="img-container">
          <img :src="profileImage" class="img-fluid rounded-circle" alt="Profile Picture" />
        </div>
      </div>
    </div>
  </section>
</template>
