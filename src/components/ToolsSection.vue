<script setup>
const toolCategories = [
  {
    name: 'Front End',
    tools: [
      { name: 'HTML5', image: 'images/html5.png' },
      { name: 'CSS3', image: 'images/css3.png' },
      { name: 'Bootstrap', image: 'images/bootstrap.png' },
      { name: 'JavaScript', image: 'images/javascript.png' }
    ]
  },
  {
    name: 'MERN Stack',
    tools: [
      { name: 'MongoDB', image: 'images/mongodb.png' },
      { name: 'Express', image: 'images/express.png' },
      { name: 'React', image: 'images/react.png' },
      { name: 'Node.js', image: 'images/node.png' }
    ]
  },
  {
    name: 'Other Tools',
    tools: [
      { name: 'Heroku', image: 'images/heroku.png' },
      { name: 'Git', image: 'images/git.png' },
      { name: 'Postman', image: 'images/postman.png' },
      { name: 'Sublime', image: 'images/sublime.png' }
    ]
  }
]
</script>

<template>
  <section class="container-fluid text-center mt-5" id="tools">
    <h2 class="mb-2">My Tech Stack</h2>
    <p class="mb-5">Technologies I work with</p>

    <div class="row justify-content-center">
      <div class="col-lg-4 mb-5" v-for="category in toolCategories" :key="category.name">
        <div class="tools-category">
          <h3 class="h5 mb-4">{{ category.name }}</h3>
          <div class="row g-3 justify-content-center">
            <div class="col-6 col-sm-4" v-for="tool in category.tools" :key="tool.name">
              <div class="tool-card">
                <img :src="tool.image" class="img-fluid tool-icon" :alt="tool.name">
                <p class="tool-name mt-2 mb-0">{{ tool.name }}</p>
                <div class="skill-bar">
                  <div class="skill-progress"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
