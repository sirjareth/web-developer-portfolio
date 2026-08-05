<template>
  <!-- ===================== CONTACT ===================== -->
  <section id="contact">
    <div class="container">
      <span class="section-label">Get In Touch</span>
      <h2 class="section-title">Contact <span>Me</span></h2>

      <div class="row g-4 align-items-stretch">

        <!-- Map -->
        <div class="col-lg-6">
          <div class="contact-map-placeholder h-100">
            <iframe 
              src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d124207.67247498203!2d121.11236869692398!3d13.38197181844695!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x33bce8d27f6f844d%3A0xf7cc1b1c943ab71b!2sCalapan%20City%2C%20Oriental%20Mindoro!5e0!3m2!1sen!2sph!4v1776055064470!5m2!1sen!2sph" 
              width="600" 
              height="450" 
              allowfullscreen="" 
              loading="lazy" 
              referrerpolicy="no-referrer-when-downgrade">
            </iframe>
          </div>
        </div>

        <!-- Form -->
        <div class="col-lg-6">
          <div class="contact-form">
            <div class="mb-3">
              <input
                v-model="name"
                type="text"
                class="form-control"
                placeholder="Your Name"
              />
            </div>
            <div class="mb-3">
              <input
                v-model="email"
                type="email"
                class="form-control"
                placeholder="Your Email"
              />
            </div>
            <div class="mb-3">
              <input
                v-model="subject"
                type="text"
                class="form-control"
                placeholder="Subject"
              />
            </div>
            <div class="mb-4">
              <textarea
                v-model="message"
                class="form-control"
                placeholder="Your Message"
                rows="5"
              ></textarea>
            </div>

            <!-- @click instead of onclick -->
            <button
              type="button"
              class="btn-primary-custom"
              @click="handleFormSubmit"
            >
              Send Message
            </button>
          </div>

          <!-- Socials -->
          <div class="d-flex gap-2 mt-4">
            <a href="https://github.com/sirjareth" class="social-btn" title="GitHub" target="_blank">GH</a>
            <a href="https://www.linkedin.com/feed/" class="social-btn" title="LinkedIn" target="_blank">in</a>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const name = ref('')
const email = ref('')
const subject = ref('')
const message = ref('')

const handleFormSubmit = () => {
  if (!name.value || !email.value || !subject.value || !message.value) {
    alert('Please fill in all fields before sending.')
    return
  }

  alert('Message sent! (Connect your backend to process this.)')

  // Clear form
  name.value = ''
  email.value = ''
  subject.value = ''
  message.value = ''
}
</script>