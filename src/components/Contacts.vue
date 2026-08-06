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
              width="600" height="450" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade">
            </iframe>
          </div>
        </div>

        <!-- Form -->
        <div class="col-lg-6">
          <div class="contact-form">
            <div class="mb-3">
              <input v-model="name" type="text" class="form-control" placeholder="Your Name" />
            </div>
            <div class="mb-3">
              <input v-model="email" type="email" class="form-control" placeholder="Your Email" />
            </div>
            <div class="mb-3">
              <input v-model="subject" type="text" class="form-control" placeholder="Subject" />
            </div>
            <div class="mb-4">
              <textarea v-model="message" class="form-control" placeholder="Your Message" rows="5"></textarea>
            </div>

            <button type="button" class="btn-primary-custom" @click="submitForm" :disabled="isLoading">
              {{ isLoading ? "Sending..." : "Send Message" }}
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
import { ref, onMounted, onBeforeUnmount } from "vue";

import { Notyf } from "notyf";
import "notyf/notyf.min.css";

const notyf = new Notyf();

const WEB3FORMS_ACCESS_KEY = "1c28a6b3-1a75-438b-9ad5-cfd291b53fa0";
const SITE_KEY = "6LdgrP0sAAAAALGoO-96sOmvUtdnCZmnaJEOaihh";

const emailSubject = "New message from Portfolio Contact Form";

const name = ref("");
const email = ref("");
const subject = ref("");
const message = ref("");

const isLoading = ref(false);

/* ---------------------- reCAPTCHA ---------------------- */

const recaptchaContainer = ref(null);
const recaptchaWidgetId = ref(null);
const recaptchaToken = ref("");

function onRecaptchaSuccess(token) {
  recaptchaToken.value = token;
}

function onRecaptchaExpired() {
  recaptchaToken.value = "";
}

function renderRecaptcha() {
  if (!window.grecaptcha || !recaptchaContainer.value) {
    return;
  }

  recaptchaWidgetId.value = window.grecaptcha.render(
    recaptchaContainer.value,
    {
      sitekey: SITE_KEY,
      callback: onRecaptchaSuccess,
      "expired-callback": onRecaptchaExpired,
    }
  );
}

function resetRecaptcha() {
  if (recaptchaWidgetId.value !== null) {
    window.grecaptcha.reset(recaptchaWidgetId.value);
    recaptchaToken.value = "";
  }
}

/* ---------------------- Submit Form ---------------------- */

const submitForm = async () => {
  if (!name.value.trim()) {
    notyf.error("Please enter your name.");
    return;
  }

  if (!email.value.trim()) {
    notyf.error("Please enter your email.");
    return;
  }

  if (!message.value.trim()) {
    notyf.error("Please enter your message.");
    return;
  }

  // if (!recaptchaToken.value) {
  //   notyf.error("Please verify that you are not a robot.");
  //   return;
  // }

  isLoading.value = true;

  try {
    const response = await fetch("https://api.web3forms.com/submit", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
      body: JSON.stringify({
        access_key: WEB3FORMS_ACCESS_KEY,
        subject: subject.value
          ? `${emailSubject} - ${subject.value}`
          : emailSubject,
        name: name.value,
        email: email.value,
        message: message.value,
      }),
    });

    const result = await response.json();

    if (result.success) {
      notyf.success("Message sent successfully!");

      name.value = "";
      email.value = "";
      subject.value = "";
      message.value = "";

      resetRecaptcha();
    } else {
      notyf.error("Failed to send message.");
    }
  } catch (error) {
    console.error(error);
    notyf.error("Something went wrong.");
  } finally {
    isLoading.value = false;
  }
};

/* ---------------------- Lifecycle ---------------------- */

let interval = null;

onMounted(() => {
  interval = setInterval(() => {
    if (window.grecaptcha && window.grecaptcha.render) {
      renderRecaptcha();
      clearInterval(interval);
    }
  }, 100);
});

onBeforeUnmount(() => {
  if (interval) {
    clearInterval(interval);
  }
});
</script>