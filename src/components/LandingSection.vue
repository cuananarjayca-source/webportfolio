<script setup>
const name = 'Arjay'
const tagline = "I'm an aspiring Full Stack Web Developer"
const bio = `A visionary Product Designer and Systems Architect with a specialized focus on
monochromatic UX/UI ecosystems. Known for transforming complex logistics—from
international airline booking systems to end-to-end data science capstones—into
seamless, single-hue digital experiences.`
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
