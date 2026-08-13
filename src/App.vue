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
          <svg class="menu-icon" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
            <path class="menu-icon-line line1" d="M4 7h16" />
            <path class="menu-icon-line line2" d="M4 12h16" />
            <path class="menu-icon-line line3" d="M4 17h16" />
          </svg>
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
            <div class="profile-tags social-links" aria-label="Social links">
              <a href="https://www.facebook.com/amlan.mandol" title="Facebook" aria-label="Facebook" target="_blank" rel="noopener noreferrer" class="social-link">
                <svg width="35" height="35" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
                  <rect x="0" y="0" width="24" height="24" rx="5" fill="var(--social-bg,#1877F2)" />
                  <path fill="var(--social-fg,#fff)" d="M15.12 8.05h-1.64V6.53c0-.45.3-.56.5-.56h1.13V3.2h-1.55C12.8 3.2 12 3.91 12 5.26v2.79H10v2.96h2v7.03h2.99v-7.03h1.99l.24-2.96z" />
                </svg>
              </a>

              <a href="https://www.instagram.com/amlan.mandol" title="Instagram" aria-label="Instagram" target="_blank" rel="noopener noreferrer" class="social-link">
                <svg width="35" height="35" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
                  <rect x="0" y="0" width="24" height="24" rx="5" fill="var(--social-bg,#E1306C)" />
                  <path fill="var(--social-fg,#fff)" d="M7 2h10a5 5 0 015 5v10a5 5 0 01-5 5H7a5 5 0 01-5-5V7a5 5 0 015-5zm5 6.5A4.5 4.5 0 1016.5 13 4.5 4.5 0 0012 8.5zM18.5 6a1.5 1.5 0 11-1.5-1.5A1.5 1.5 0 0118.5 6z" />
                </svg>
              </a>

              <a href="https://wa.me/8801733472747" title="WhatsApp" aria-label="WhatsApp" target="_blank" rel="noopener noreferrer" class="social-link">
                <svg width="35" height="35" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
                  <rect x="0" y="0" width="24" height="24" rx="5" fill="var(--social-bg,#25D366)" />
                  <path fill="var(--social-fg,#fff)" d="M20.52 3.48A11.8 11.8 0 0012 .5C5.73.5.5 5.73.5 12a11.8 11.8 0 002.96 7.52L3 23l3.54-1A11.8 11.8 0 0012 23.5c6.27 0 11.5-5.23 11.5-11.5 0-3.07-1.2-5.92-3.98-8.52zM12 20a8 8 0 01-4.45-1.3l-.32-.2-2.64.82.82-2.63-.2-.33A8 8 0 1112 20zm3.2-5.1c-.18-.09-1.06-.52-1.22-.58-.16-.06-.28.09-.4.09-.12.18-.47.58-.57.7-.1.12-.2.13-.38.05-.18-.08-.76-.28-1.45-.9-.54-.48-.9-1.08-1-1.26-.11-.18-.01-.28.08-.37.08-.08.18-.2.27-.3.09-.1.12-.18.18-.3.06-.12.03-.22-.02-.31-.05-.09-.4-1.01-.55-1.38-.14-.36-.28-.31-.38-.31-.1 0-.22-.01-.34-.01-.12 0-.31.05-.47.22-.16.17-.62.6-.62 1.46 0 .86.64 1.68.73 1.79.09.11 1.25 1.93 3.02 2.76 1.28.63 2.3.89 3.09 1.01.43.06.82.05 1.13.03.34-.03 1.06-.43 1.21-.85.15-.42.15-.78.11-.85-.05-.07-.18-.11-.37-.2z" />
                </svg>
              </a>

              <a href="https://www.linkedin.com/in/amlan-kumar-mandol-644b061b8" title="LinkedIn" aria-label="LinkedIn" target="_blank" rel="noopener noreferrer" class="social-link">
                <svg width="35" height="35" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
                  <rect x="0" y="0" width="24" height="24" rx="5" fill="var(--social-bg,#0077B5)" />
                  <path fill="var(--social-fg,#fff)" d="M6.94 8.5H4.5V20h2.44V8.5zM5.72 6.9a1.45 1.45 0 110-2.9 1.45 1.45 0 010 2.9zM20 20h-2.44v-5.6c0-1.33-.03-3.04-1.85-3.04-1.85 0-2.13 1.44-2.13 2.93V20H11.6V8.5h2.34v1.56h.03c.33-.62 1.14-1.27 2.35-1.27 2.51 0 2.97 1.65 2.97 3.79V20z" />
                </svg>
              </a>

              <a href="https://github.com/AKmandol" title="GitHub" aria-label="GitHub" target="_blank" rel="noopener noreferrer" class="social-link">
                <svg width="35" height="35" viewBox="0 0 24 24" aria-hidden="true" focusable="false">
                  <rect x="0" y="0" width="24" height="24" rx="5" fill="var(--social-bg,#24292e)" />
                  <path fill="var(--social-fg,#fff)" d="M12 .5C5.73.5.5 5.73.5 12c0 5.08 3.29 9.38 7.86 10.9.58.11.79-.25.79-.56 0-.28-.01-1.02-.02-2-3.2.7-3.88-1.5-3.88-1.5-.52-1.33-1.27-1.69-1.27-1.69-1.04-.71.08-.7.08-.7 1.15.08 1.75 1.18 1.75 1.18 1.02 1.75 2.68 1.25 3.33.96.1-.75.4-1.25.73-1.54-2.56-.29-5.26-1.28-5.26-5.69 0-1.26.45-2.29 1.18-3.1-.12-.29-.51-1.45.11-3.03 0 0 .97-.31 3.18 1.18a11.06 11.06 0 012.9-.39c.98 0 1.97.13 2.9.39 2.2-1.49 3.17-1.18 3.17-1.18.62 1.58.23 2.74.11 3.03.73.81 1.18 1.84 1.18 3.1 0 4.42-2.71 5.39-5.29 5.68.41.35.77 1.04.77 2.1 0 1.52-.01 2.75-.01 3.12 0 .31.21.68.8.56A10.52 10.52 0 0023.5 12C23.5 5.73 18.27.5 12 .5z" />
                </svg>
              </a>
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
        <i class="skill-li"></i>
        <img class="skill-img" src="/logo/p2.png" alt="">
        <i class="skill-li"></i>
        <img class="skill-img" src="/logo/p3.png" alt="">
        <i class="skill-li"></i>
        <img class="skill-img" src="/logo/p4.png" alt="">
        <i class="skill-li"></i>
        <img class="skill-img p-1" src="/logo/p6.png" alt="">
        <i class="skill-li"></i>
        <img class="skill-img" src="/logo/p7.png" alt="">
        <i class="skill-li"></i>
        <img class="skill-img p-1" src="/logo/p5.png" alt="">
        <i class="skill-li"></i>
        <img class="skill-img p-1" src="/logo/p8.png" alt="">
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