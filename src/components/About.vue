<script setup>
  const proofStats = [
    {
      value: "03+",
      label: "Years experience",
    },
    {
      value: "15+",
      label: "Systems delivered",
    },
    {
      value: "08+",
      label: "API integrations",
    },
  ];

  const capabilities = [
    {
      index: "01",
      title: "Backend Systems",
      description: "APIs, business rules and secure service logic.",
      tools: "Laravel / PHP / AdonisJS / Node.js / REST / JWT / MySQL / Redis / MongoDB / PostgreSQL / Firebase",
    },
    {
      index: "02",
      title: "Product Interfaces",
      description: "Dashboards and workflows built for daily use.",
      tools: "Vue.js / React.js / iView / Vuetify / ApexCharts / Tailwind / Bootstrap",
    },
    {
      index: "03",
      title: "Payments & Integrations",
      description: "Gateways, webhooks and traceable payment states.",
      tools: "Stripe / SSLCommerz / OvyPay / CheezyPay / G-Pay / Pay Agency / BennuPay / CheezyPay",
    },
    {
      index: "04",
      title: "Delivery & Operations",
      description: "Deployments, server setup and release workflow.",
      tools: "Linux / Nginx / PM2 / cPanel / Git / GitHub / GitLab / CI/CD / Docker",
    },
  ];
</script>

<template>
  <section id="about" class="section about-section">
    <div class="section-index">
      <span>02</span>
      About
    </div>

    <div class="about-content">
      <p class="lead">
        Complex requirements.
        <strong>Clear software.</strong>
      </p>

    </div>

    <div class="proof-grid" aria-label="Professional proof points">
      <article v-for="item in proofStats" :key="item.label">
        <strong>{{ item.value }}</strong>
        <span>{{ item.label }}</span>
      </article>
    </div>

    <div class="capability-list">
      <article v-for="capability in capabilities" :key="capability.title" class="capability-row">
        <span class="capability-index">{{ capability.index }}</span>
        <div>
          <h3>{{ capability.title }}</h3>
          <p>{{ capability.description }}</p>
        </div>
        <strong>{{ capability.tools }}</strong>
      </article>
    </div>
  </section>
</template>