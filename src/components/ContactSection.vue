<script setup>
import { reactive } from 'vue'

const form = reactive({
  name: '',
  email: '',
  phone: '',
  message: ''
})

const contactInfo = [
  { label: 'Email', icon: 'bi bi-envelope-fill', href: 'mailto:arjay@example.com', value: 'arjay@example.com' },
  { label: 'Phone', icon: 'bi bi-telephone-fill', href: 'tel:+1234567890', value: '+123 456 7890' },
  { label: 'Location', icon: 'bi bi-geo-alt-fill', href: null, value: 'Manila, Philippines' }
]

const socialLinks = [
  { label: 'LinkedIn', icon: 'bi bi-linkedin', url: 'https://linkedin.com/' },
  { label: 'GitHub', icon: 'bi bi-github', url: 'https://github.com/' },
  { label: 'GitLab', icon: 'bi bi-gitlab', url: 'https://gitlab.com/' }
]

const handleSubmit = () => {
  console.log('Form submitted:', form)
  alert('Message sent! (Wire up your preferred form service here.)')
  form.name = ''
  form.email = ''
  form.phone = ''
  form.message = ''
}
</script>

<template>
  <section class="container-fluid p-0" id="contact">
    <div class="row g-0">

      <!-- Left Side - Contact Info -->
      <div class="col-lg-6 contact-info-side">
        <div class="contact-info-wrapper">
          <h2 class="display-4 mb-4">Let's Work Together!</h2>
          <p class="lead mb-5">Have a project in mind? Let's make it happen!</p>

          <div class="contact-details">
            <div class="contact-item" v-for="item in contactInfo" :key="item.label">
              <div class="contact-icon">
                <i :class="item.icon"></i>
              </div>
              <div>
                <h5>{{ item.label }}</h5>
                <a v-if="item.href" :href="item.href">{{ item.value }}</a>
                <p v-else>{{ item.value }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Right Side - Contact Form -->
      <div class="col-lg-6 contact-form-side">
        <div class="contact-form-wrapper">
          <h3 class="mb-4 text-center">Send Me a Message</h3>

          <form class="modern-form" @submit.prevent="handleSubmit">
            <div class="form-floating mb-3">
              <input
                type="text"
                class="form-control"
                id="name"
                placeholder="Name"
                v-model="form.name"
                required
              />
              <label for="name">Full Name</label>
            </div>

            <div class="form-floating mb-3">
              <input
                type="email"
                class="form-control"
                id="email"
                placeholder="Email"
                v-model="form.email"
                required
              />
              <label for="email">Email Address</label>
            </div>

            <div class="form-floating mb-3">
              <input
                type="tel"
                class="form-control"
                id="phone"
                placeholder="Phone"
                v-model="form.phone"
              />
              <label for="phone">Phone (Optional)</label>
            </div>

            <div class="form-floating mb-4">
              <textarea
                class="form-control"
                id="message"
                placeholder="Message"
                v-model="form.message"
                required
              ></textarea>
              <label for="message">Your Message</label>
            </div>

            <button type="submit" class="btn btn-submit-modern w-100">
              <span>Send Message</span>
              <i class="bi bi-send-fill ms-2"></i>
            </button>
          </form>

          <!-- Social Media -->
          <div class="social-links-large mt-5">
            <h5 class="mb-3">Follow Me</h5>
            <a
              v-for="social in socialLinks"
              :key="social.label"
              :href="social.url"
              target="_blank"
              rel="noopener noreferrer"
              class="social-btn"
            >
              <i :class="social.icon"></i>
              <span>{{ social.label }}</span>
            </a>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>
