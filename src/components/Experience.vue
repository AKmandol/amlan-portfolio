<script setup>
  import { ref } from "vue";
  const defaultExperiences = [
    {
      company: "Netcoden Inc.",
      role: "Software Engineer",
      duration: "Aug 2023 - Jul 2026",
      location: "Dhaka, Bangladesh",
      summary: "Building CRM, partner and payment systems.",
      points: [
        "Laravel / AdonisJS / Node / Vue.js application builds.",
        "CRM and partner modules.",
        "Crypto and card payment flows.",
        "Releases and Linux operations.",
        "API integrations and webhooks.",
        "Database design and query optimization.",
        "Performance monitoring and troubleshooting.",
        "CI/CD and Git workflow.",
        "System architecture and design.",
        "Team collaboration and code reviews.",
        "Client communication and requirement gathering.",
      ],
    },
    {
      company: "Tech Solution IT Ltd.",
      role: "Full-Stack Developer",
      duration: "May 2022 - Jun 2023",
      location: "Dhaka, Bangladesh",
      summary: "Delivered Laravel and Vue client applications.",
      points: [
        "Laravel / AdonisJS / Vue.js / WP application builds.",
        "Database design and query improvement.",
        "Payments, analytics and CRM integrations.",
        "System architecture and design.",
        "Client communication and requirement gathering.",
      ],
    },
  ];
  const experiences = ref(defaultExperiences);
</script>

<template>
  <div class="experience">
    <section id="experience" class="section experience-section">
      <div class="section-heading">
        <div class="section-index">
          <span>03</span>
          Experience
        </div>
        <div>
          <h2>Experience shipping production systems.</h2>
        </div>
      </div>

      <div class="experience-list">
        <article
          v-for="exp in experiences"
          :key="exp.company"
          class="experience-item"
        >
          <div class="experience-period">
            <span>{{ exp.duration }}</span>
            <small>{{ exp.location }}</small>
          </div>

          <div class="experience-role">
            <div class="experience-title-row">
              <span>{{ exp.company }}</span>
              <small>{{ exp.location }}</small>
            </div>
            <h3>{{ exp.role }}</h3>
            <p>{{ exp.summary }}</p>
          </div>

          <ul>
            <li v-for="point in exp.points" :key="point">{{ point }}</li>
          </ul>
        </article>
      </div>
    </section>
  </div>
</template>
