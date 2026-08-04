<script setup>
import { ref } from "vue";

const mobileMenuOpen = ref(false);

const defaultProjects = [
  {
    number: "01",
    title: "CRM System",
    category: "Customer Relationship Management",
    description:
      "A CRM system designed to help businesses manage customer interactions and data effectively.",
    problem:
      "The client needed a solution to track customer interactions, manage leads, and improve customer relationships.",
    contribution:
      "Developed the CRM backend, implemented lead management features, and created dashboards for analytics.",
    result:
      "The CRM system improved customer engagement and provided valuable insights into customer behavior.",
    role: "Software Engineer",
    tech: ["Laravel", "AdonisJS", "Vue.js", "MySQL"],
    accent: "orange",
    link: "https://forexcrm.ca",
    image: "/project/forex.png",
  },
  {
    number: "02",
    title: "Payment Services",
    category: "Fintech & Payments",
    description:
      "A service that integrates various payment gateways for seamless transactions.",
    problem:
      "The client required a unified payment solution to handle multiple payment methods and ensure secure transactions.",
    contribution:
      "Integrated multiple payment gateways, implemented transaction tracking, and ensured compliance with security standards.",
    result:
      "The service enabled smooth payment processing and enhanced the overall user experience.",
    role: "Backend Developer",
    tech: ["AdonisJS", "Node.js", "Vue.js"],
    accent: "purple",
    link: "https://ovypay.com",
    image: "/project/ovy.jpg",
  },
  {
    number: "03",
    title: "Travel Agency System",
    category: "Travel & Booking",
    description:
      "A comprehensive travel agency system for managing bookings, payments, and customer interactions.",
    problem:
      "The client needed a robust system to handle complex travel bookings and integrate multiple payment gateways.",
    contribution:
      "Developed the backend APIs, integrated payment gateways, and built the user interface for managing bookings.",
    result:
      "The system streamlined the booking process, improved customer satisfaction, and increased revenue.",
    role: "Full-Stack Developer",
    tech: ["Laravel", "Vue.js", "SSLCommerz", "MySQL"],
    accent: "blue",
    link: "https://tour.amlanbd.com",
    image: "/project/tour.webp",
  },
  {
    number: "04",
    title: "E-Commerce Platform",
    category: "Retail & E-Commerce",
    description:
      "An e-commerce platform that allows users to browse products, make purchases, and track orders.",
    problem:
      "The client required a scalable e-commerce solution with secure payment processing and order management.",
    contribution:
      "Implemented the product catalog, shopping cart, checkout process, and integrated multiple payment options.",
    result:
      "The platform increased online sales and provided a seamless shopping experience for customers.",
    role: "Backend Developer",
    tech: ["Laravel", "Vue.js", "Stripe", "MySQL"],
    accent: "green",
    link: "https://ecom.amlanbd.com",
    image: "/project/ecom.webp",
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

const skillGroups = [
  {
    title: "Laravel",
    logo: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-original.svg",
    items: ["Backend", "REST APIs", "Auth", "Services"],
  },
  {
    title: "Vue.js",
    logo: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg",
    items: ["SPA", "Components", "Dashboards", "Vuex"],
  },
  {
    title: "MySQL",
    logo: "https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg",
    items: ["Schema", "Queries", "Relations", "Tuning"],
  },
  {
    title: "cPanel",
    logo: "https://cdn.worldvectorlogo.com/logos/cpanel.svg",
    items: ["Hosting", "Domains", "Email", "Server Tools"],
  },
  {
    title: "Stripe",
    logo: "https://cdn.worldvectorlogo.com/logos/stripe-4.svg",
    items: ["Payments", "Checkout", "Webhooks", "States"],
  },
];

const defaultExperiences = [
  {
    company: "Netcoden Inc.",
    role: "Software Engineer",
    duration: "Aug 2023 - Jul 2026",
    location: "Dhaka, Bangladesh",
    summary:
      "Building CRM, partner and payment systems.",
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
      "Client communication and requirement gathering."
    ],
  },
  {
    company: "Tech Solution IT Ltd.",
    role: "Full-Stack Developer",
    duration: "May 2022 - Jun 2023",
    location: "Dhaka, Bangladesh",
    summary:
      "Delivered Laravel and Vue client applications.",
    points: [
      "Laravel / AdonisJS / Vue.js / WP application builds.",
      "Database design and query improvement.",
      "Payments, analytics and CRM integrations.",
      "System architecture and design.",
      "Client communication and requirement gathering."
    ],
  },
];

const form = ref({
  name: "",
  email: "",
  message: "",
});

const loading = ref(false);
const success = ref("");
const error = ref("");
const cvUrl = "/Amlan-Kumar-Mandol-CV.pdf";
const cvPreviewUrl = "/amlan-kumar-mandol-cv.html";

const projects = ref(defaultProjects);
const experiences = ref(defaultExperiences);

const formatProjectNumber = (value, index) => {
  if (value) {
    return String(value).padStart(2, "0");
  }

  return String(index + 1).padStart(2, "0");
};

const closeMenu = () => {
  mobileMenuOpen.value = false;
};

const submitContact = () => {
  error.value = "";
  success.value = "";

  if (!form.value.name.trim() || !form.value.email.trim() || !form.value.message.trim()) {
    error.value = "Please complete all fields.";
    return;
  }

  const mailto = `mailto:amlankumar47@gmail.com?subject=${encodeURIComponent(
    `Contact from ${form.value.name}`
  )}&body=${encodeURIComponent(
    `Name: ${form.value.name}\nEmail: ${form.value.email}\n\n${form.value.message}`
  )}`;

  window.location.href = mailto;
};
</script>

<template>
  <div class="site-shell">
    <div class="ambient ambient-one"></div>
    <div class="ambient ambient-two"></div>

    <header class="site-header">
      <nav class="navbar" aria-label="Primary navigation">
        <a class="brand" href="#top" aria-label="Amlan Kumar Mandol, home" @click="closeMenu">
          <p class="icon-image"></p>
          <span class="brand-copy">
            <strong>Amlan Kumar Mandol</strong>
            <small>Software Engineer</small>
          </span>
        </a>

        <button class="menu-toggle" type="button" :aria-expanded="mobileMenuOpen" aria-label="Toggle navigation"
          @click="mobileMenuOpen = !mobileMenuOpen">
          <span></span>
          <span></span>
        </button>

        <div class="nav-links" :class="{ open: mobileMenuOpen }">
          <a href="#about" @click="closeMenu">About</a>
          <a href="#projects" @click="closeMenu">Work</a>
          <a href="#experience" @click="closeMenu">Experience</a>
          <a class="nav-cta" href="#contact" @click="closeMenu">
            Hire me
          </a>
        </div>
      </nav>
    </header>

    <main id="top">
      <section class="hero">
        <div class="hero-copy">
          <div class="availability">
            <span class="availability-dot"></span>
            Available for software engineer roles
          </div>

          <p class="hero-kicker">Laravel, Node/AdonisJS, Vue.js, Git, CI/CD, AI engineer</p>

          <h1>
            I build practical software
            <em>companies can trust.</em>
          </h1>


          <div class="profile-card" aria-label="Professional profile summary">
            <div class="profile-avatar">
              <p class="avatar-initials">AKM</p>
            </div>
            <div class="profile-card-copy">
              <span>Full-Stack Software Engineer</span>
              <strong>Amlan Kumar Mandol</strong>
              <p>Laravel / AdonisJS / Node / Vue.js / React.js / Git </p>
              <p>-- Dhaka, Bangladesh</p>
            </div>
            <div class="profile-tags" aria-label="Primary strengths">
              <span>CRM</span>
              <span>E-Commerce</span>
              <span>Travel Agency</span>
              <span>Payments</span>
              <span>Dashboards</span>
            </div>
          </div>

          <div class="hero-actions">
            <a :href="cvUrl" download class="button button-primary button-large">
              Download CV
            </a>
            <a href="#projects" class="button button-secondary button-large">
              See my work
            </a>
          </div>

        </div>

        <div class="hero-visual" aria-hidden="true">

          <div class="hexagon-wrapper">
            <div class="hexagon-shape">
              <img src="/me.png" alt="Profile" class="profile-img" />
            </div>
          </div>
        </div>
      </section>

      <div class="trust-strip" aria-label="Areas of expertise">
        <img class="skill-img p-1" src="/logo/p1.png" alt="">
        <i></i>
        <img class="skill-img" src="/logo/p2.png" alt="">
        <i></i>
        <img class="skill-img" src="/logo/p3.png" alt="">
        <i></i>
        <img class="skill-img" src="/logo/p4.png" alt="">
        <i></i>
        <img class="skill-img p-1" src="/logo/p6.png" alt="">
        <i></i>
        <img class="skill-img" src="/logo/p7.png" alt="">
        <i></i>
        <img class="skill-img p-1" src="/logo/p5.png" alt="">
      </div>

      <section id="projects" class="section projects-section">
        <div class="section-heading">
          <div class="section-index">
            <span>01</span>
            Selected work
          </div>
          <div>
            <h2>Selected systems with real business use.</h2>
          </div>
        </div>

        <div class="project-list">
          <article v-for="project in projects" :key="project.title" class="project-card"
            :class="`accent-${project.accent}`">
            <div class="project-topline">
              <div>
                <span class="project-number">{{ project.number }}</span>
                <span class="project-category">{{ project.category }}</span>
              </div>
              <span class="project-status">
                <i></i>
                Case study
              </span>
            </div>

            <div class="project-visual" aria-hidden="true">
              <div class="visual-system">
                <img :src="project.image" :alt="`Project visual: ${project.title}`" class="project-visual-img" />
                <div class="system-node node-primary">
                  <small>Core</small>
                  <strong>{{ project.tech[0] }}</strong>
                </div>
                <span class="system-line line-one"></span>
                <span class="system-line line-two"></span>
                <div class="system-node node-secondary">
                  <small>Interface</small>
                  <strong>{{ project.tech[1] }}</strong>
                </div>
                <div class="system-node node-tertiary">
                  <small>Integration</small>
                  <strong>{{ project.tech[2] }}</strong>
                </div>
              </div>
            </div>

            <div class="project-body">
              <h3>{{ project.title }}</h3>
              <p>{{ project.description }}</p>
            </div>

            <div class="project-proof">
              <div class="proof-item">
                <span>Problem</span>
                <strong>{{ project.problem }}</strong>
              </div>
              <div class="proof-item">
                <span>My role</span>
                <strong>{{ project.role }}</strong>
              </div>
              <div class="proof-item">
                <span>Shipped</span>
                <strong>{{ project.contribution }}</strong>
              </div>
              <div class="proof-item">
                <span>Result</span>
                <strong>{{ project.result }}</strong>
              </div>
            </div>

            <div class="project-meta">
              <div class="tech-list">
                <span v-for="item in project.tech" :key="item">{{ item }}</span>
              </div>
              <a class="project-link" target="_blank" :href="project.link">
                View project
              </a>
            </div>

          </article>
        </div>
      </section>

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
            <article v-for="exp in experiences" :key="exp.company" class="experience-item">
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
                    d="M6.6 10.8c1.4 2.8 3.8 5.2 6.6 6.6l2.2-2.2c.3-.3.8-.4 1.2-.3 1.3.4 2.6.6 4 .6.7 0 1.2.5 1.2 1.2v3.5c0 .7-.5 1.2-1.2 1.2C10.3 21.9 2.1 13.7 2.1 3.4c0-.7.5-1.2 1.2-1.2h3.5c.7 0 1.2.5 1.2 1.2 0 1.4.2 2.7.6 4 .1.4 0 .9-.3 1.2l-1.7 2.2Z" />
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
                    d="M4 5h16c1.1 0 2 .9 2 2v10c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V7c0-1.1.9-2 2-2Zm8 8.1L20 8V7.7l-8 5.1-8-5.1V8l8 5.1Z" />
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
            <input v-model="form.name" type="text" name="name" autocomplete="name"
              placeholder="How should I address you?" />
          </label>

          <label>
            <span>Email address</span>
            <input v-model="form.email" type="email" name="email" autocomplete="email" placeholder="you@company.com" />
          </label>

          <label>
            <span>Project details</span>
            <textarea v-model="form.message" name="message" rows="10"
              placeholder="Tell me about the product, scope or problem..."></textarea>
          </label>

          <button type="submit" :disabled="loading">
            <span>{{ loading ? "Sending..." : "Send" }}</span>
          </button>

          <p v-if="success" class="form-message success" role="status">{{ success }}</p>
          <p v-if="error" class="form-message error" role="alert">{{ error }}</p>
        </form>
      </section>
    </main>

    <footer class="site-footer">
      <a class="brand footer-brand" href="#top" aria-label="Back to top">
        <span class="text-logo">AKM</span>
        <span class="brand-copy">
          <strong>Amlan Kumar Mandol</strong>
          <small>Full-Stack Software Engineer</small>
        </span>
      </a>

      <p>Building reliable software for ambitious businesses.</p>

      <a class="back-to-top" href="#top">
        Back to top
      </a>
    </footer>
  </div>
</template>
