<script setup>
    import {Notyf} from 'notyf';
    import {ref, reactive, onMounted, onBeforeUnmount} from 'vue';

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

    const notyf = new Notyf();

    const name = ref("");
    const phone = ref("");
    const email = ref("");
    const message = ref("");

    const isLoading = ref(false);
    const WEB3FORMS_ACCESS_KEY = "c1b6e2f5-890d-43da-ac37-271a096a038c";

    const subject = "New message from Portfolio Contact Form";
    const submitForm = async () => {

        if (!recaptchaToken.value) {
            notyf.error("Please verify that you are not a robot.");
            return;
        }

        isLoading.value = true;

        try {
            const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json"
                },
                body: JSON.stringify({
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    name: name.value,
                    phone: phone.value,
                    email: email.value,
                    message: message.value
                })
            })
            const result = await response.json();
            if (result.success) {
                console.log(result);
                isLoading.value = false;
                notyf.success("Message Sent!");
            }
        } catch (error) {
            console.log(error);
            isLoading.value = false;
            notyf.error("Failed to send message.");
        } finally {
            resetRecaptcha();
        }
    }

    /*reCAPTCHA Integration*/

    const SITE_KEY = '6LeEegctAAAAAPnNKcEbDtadBvIHaYkLg2pZddpM';  // Replace with your site key
    const recaptchaContainer = ref(null);
    const recaptchaWidgetId = ref(null);
    const recaptchaToken = ref('');

    function onRecaptchaSuccess(token) {
        recaptchaToken.value = token;
    }

    function onRecaptchaExpired() {
        recaptchaToken.value = '';
    }

    function renderRecaptcha() {
        if (!window.grecaptcha) {
            console.error('reCAPTCHA not loaded');
            return;
        }

        recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
            sitekey: SITE_KEY,
            size: 'normal',
            callback: onRecaptchaSuccess,
            'expired-callback': onRecaptchaExpired,
        });
    }

    function resetRecaptcha() {
        if (recaptchaWidgetId.value !== null) {
            window.grecaptcha.reset(recaptchaWidgetId.value);
            recaptchaToken.value = '';
        }
    }

    onMounted(() => {
    const interval = setInterval(() => {
        if (window.grecaptcha && window.grecaptcha.render) {
            renderRecaptcha();
            clearInterval(interval);
        }
    }, 100);

        onBeforeUnmount(() => {
            clearInterval(interval);
        });
    }); 
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

          <form class="modern-form" @submit.prevent="submitForm">
            <div class="form-floating mb-3">
              <input
                type="text"
                class="form-control"
                id="name"
                placeholder="Name"
                v-model="name"
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
                v-model="email"
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
                v-model="phone"
              />
              <label for="phone">Phone (Optional)</label>
            </div>

            <div class="form-floating mb-4">
              <textarea
                class="form-control"
                id="message"
                placeholder="Message"
                v-model="message"
                required
              ></textarea>
              <label for="message">Your Message</label>
            </div>

            <div class="grecaptcha d-flex justify-content-start mb-3">
                <div ref="recaptchaContainer"></div>
            </div>

            <button type="submit" class="btn btn-submit-modern w-100" :disabled="isLoading">
              <span>{{ isLoading ? 'Sending ...' : 'Submit ' }}</span>
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
