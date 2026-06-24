<template>
  <footer id="footer">
    <div class="container">
      <div class="footer-content">

        <!-- Brand Column -->
        <div class="footer-column">
          <h3 class="footer-brand">Arjay</h3>
          <p class="footer-tagline">Full Stack Web Developer</p>
          <p class="footer-description">
            Creating seamless digital experiences with modern web technologies.
          </p>
          <div class="footer-social mt-4">
            <a
              v-for="social in socialLinks"
              :key="social.label"
              :href="social.url"
              target="_blank"
              rel="noopener noreferrer"
              class="social-link"
            >
              <i :class="social.icon"></i>
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div class="footer-column">
          <h4 class="footer-title">Quick Links</h4>
          <ul class="footer-links">
            <li v-for="link in quickLinks" :key="link.label">
              <a :href="link.href"><i class="bi bi-chevron-right"></i> {{ link.label }}</a>
            </li>
          </ul>
        </div>

        <!-- Services -->
        <div class="footer-column">
          <h4 class="footer-title">Services</h4>
          <ul class="footer-links">
            <li v-for="service in services" :key="service.label">
              <i :class="service.icon"></i> {{ service.label }}
            </li>
          </ul>
        </div>

        <!-- Contact Info -->
        <div class="footer-column">
          <h4 class="footer-title">Get In Touch</h4>
          <ul class="footer-contact">
            <li v-for="item in contactInfo" :key="item.label">
              <i :class="item.icon"></i>
              <a v-if="item.href" :href="item.href">{{ item.value }}</a>
              <span v-else>{{ item.value }}</span>
            </li>
          </ul>
        </div>

      </div>

      <!-- Footer Bottom -->
      <div class="footer-bottom">
        <div class="footer-bottom-content">
          <p class="copyright">&copy; {{ currentYear }} Arjay. All Rights Reserved.</p>
          <p class="made-with">
            Made with <i class="bi bi-heart-fill heart-beat"></i> and <i class="bi bi-cup-hot-fill"></i>
          </p>
          <div class="footer-bottom-links">
            <a href="#">Privacy Policy</a>
            <span>|</span>
            <a href="#">Terms of Service</a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
import { computed } from 'vue'

const socialLinks = [
  { label: 'LinkedIn', icon: 'bi bi-linkedin', url: 'https://linkedin.com/' },
  { label: 'GitHub', icon: 'bi bi-github', url: 'https://github.com/' },
  { label: 'GitLab', icon: 'bi bi-gitlab', url: 'https://gitlab.com/' },
  { label: 'Twitter', icon: 'bi bi-twitter', url: 'https://x.com/' }
]

const quickLinks = [
  { label: 'Home', href: '#landing' },
  { label: 'Projects', href: '#projects' },
  { label: 'Tech Stack', href: '#tools' },
  { label: 'Contact', href: '#contact' }
]

const services = [
  { label: 'Web Development', icon: 'bi bi-code-slash' },
  { label: 'Responsive Design', icon: 'bi bi-phone' },
  { label: 'Backend Solutions', icon: 'bi bi-server' },
  { label: 'UI/UX Design', icon: 'bi bi-brush' }
]

const contactInfo = [
  { label: 'Email', icon: 'bi bi-envelope-fill', href: 'mailto:arjay@example.com', value: 'arjay@example.com' },
  { label: 'Phone', icon: 'bi bi-telephone-fill', href: 'tel:+1234567890', value: '+123 456 7890' },
  { label: 'Location', icon: 'bi bi-geo-alt-fill', href: null, value: 'Manila, Philippines' }
]

const currentYear = computed(() => new Date().getFullYear())
</script>
