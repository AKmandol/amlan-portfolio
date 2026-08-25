<script setup>
  import { ref } from "vue";
  const loading = ref(false);
  const success = ref("");
  const error = ref("");
  
  const form = ref({
    name: "",
    email: "",
    message: "",
  });

  const submitContact = () => {
    error.value = "";
    success.value = "";

    if (
      !form.value.name.trim() ||
      !form.value.email.trim() ||
      !form.value.message.trim()
    ) {
      error.value = "Please complete all fields.";
      return;
    }

    const mailto = `mailto:amlankumar47@gmail.com?subject=${encodeURIComponent(
      `Contact from ${form.value.name}`,
    )}&body=${encodeURIComponent(
      `Name: ${form.value.name}\nEmail: ${form.value.email}\n\n${form.value.message}`,
    )}`;

    window.location.href = mailto;
  };
</script>

<template>
  <section id="contact" class="contact-section">
    <div class="contact-intro">
      <div class="contact-label-row">
        <div class="section-index light">
          <span>04</span>
          Contact
        </div>
        <div class="contact-availability">
          <i></i>
          Open to software engineer roles
        </div>
      </div>

      <p class="contact-kicker">Hiring a product engineer?</p>
      <h2>Let's talk about the role and expectations.</h2>
      <p class="contact-copy">
        Available for Laravel, AdonisJS, Vue.js, APIs and payment work.
      </p>

      <div class="contact-direct-phone">
        <a href="tel:+8801733472747">
          <span class="contact-card-icon" aria-hidden="true">
            <svg viewBox="0 0 24 24" focusable="false">
              <path
                d="M6.6 10.8c1.4 2.8 3.8 5.2 6.6 6.6l2.2-2.2c.3-.3.8-.4 1.2-.3 1.3.4 2.6.6 4 .6.7 0 1.2.5 1.2 1.2v3.5c0 .7-.5 1.2-1.2 1.2C10.3 21.9 2.1 13.7 2.1 3.4c0-.7.5-1.2 1.2-1.2h3.5c.7 0 1.2.5 1.2 1.2 0 1.4.2 2.7.6 4 .1.4 0 .9-.3 1.2l-1.7 2.2Z"
              />
            </svg>
          </span>
          <span class="contact-card-copy">
            <small>Phone</small>
            <strong>+8801733472747</strong>
          </span>
        </a>
      </div>

      <div class="contact-direct">
        <a href="mailto:amlankumar47@gmail.com">
          <span class="contact-card-icon" aria-hidden="true">
            <svg viewBox="0 0 24 24" focusable="false">
              <path
                d="M4 5h16c1.1 0 2 .9 2 2v10c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V7c0-1.1.9-2 2-2Zm8 8.1L20 8V7.7l-8 5.1-8-5.1V8l8 5.1Z"
              />
            </svg>
          </span>
          <span class="contact-card-copy">
            <small>Email</small>
            <strong>amlankumar47@gmail.com</strong>
          </span>
        </a>
      </div>
    </div>

    <form class="contact-form" @submit.prevent="submitContact">
      <div class="form-heading">
        <div>
          <small>Hiring enquiry</small>
          <strong>Tell me about the role or project.</strong>
        </div>
      </div>

      <label>
        <span>Your name</span>
        <input
          v-model="form.name"
          type="text"
          name="name"
          autocomplete="name"
          placeholder="How should I address you?"
        />
      </label>

      <label>
        <span>Email address</span>
        <input
          v-model="form.email"
          type="email"
          name="email"
          autocomplete="email"
          placeholder="you@company.com"
        />
      </label>

      <label>
        <span>Project details</span>
        <textarea
          v-model="form.message"
          name="message"
          rows="10"
          placeholder="Tell me about the product, scope or problem..."
        ></textarea>
      </label>

      <button type="submit" :disabled="loading">
        <span>{{ loading ? "Sending..." : "Send" }}</span>
      </button>

      <p v-if="success" class="form-message success" role="status">
        {{ success }}
      </p>
      <p v-if="error" class="form-message error" role="alert">{{ error }}</p>
    </form>
  </section>
</template>
