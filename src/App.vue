<script setup>
import { onMounted, ref } from "vue";
import {
  collection,
  addDoc,
  getDocs,
  orderBy,
  query,
  serverTimestamp,
  doc,
  setDoc
} from "firebase/firestore";
import { db } from "./firebase";
import heroVisual from "./assets/hero.png";

const mobileMenuOpen = ref(false);

const seedProjects = async () => {
  try {
    for (const project of defaultProjects) {
      await setDoc(
        doc(db, "projects", project.number),
        {
          ...project,
          order: Number(project.number),
          createdAt: serverTimestamp(),
        }
      );
    }

    console.log("Projects synced");
  } catch (err) {
    console.error(err);
  }
};

const defaultProjects = [
  {
    number: "04",
    title: "Custom E-Commerce Platform",
    category: "E-Commerce",
    description: "Custom shop, admin, checkout and reporting workflow.",
    problem: "Orders, products and payments needed one clean control panel.",
    contribution: "RBAC, catalogue, checkout, orders, reporting",
    result: "Faster admin control and clearer payment visibility.",
    role: "Full-stack delivery",
    tech: ["Laravel", "Vue.js", "MySQL", "Payment APIs"],
    accent: "rose",
    link: "https://ecom.amlanbd.com",
  },
  {
    number: "03",
    title: "BestTourInfo Booking Platform",
    category: "Travel Technology",
    description: "Travel packages, booking flow, admin tools and payment.",
    problem: "Discovery, booking and payment felt disconnected.",
    contribution: "Booking lifecycle, admin tools, payment flow",
    result: "Clearer path from package to confirmed booking.",
    role: "Laravel + Vue delivery",
    tech: ["Laravel", "Vue.js", "Stripe", "SSLCommerz"],
    accent: "amber",
    link: "http://tour.amlanbd.com",
  },
  {
    number: "01",
    title: "Crypto Deposit System",
    category: "FinTech / Payment Gateway",
    description: "Crypto deposit flow with callbacks and admin tracking.",
    problem: "Manual deposit checks slowed operations.",
    contribution: "Gateway, webhooks, transaction states",
    result: "Less manual verification. Better audit trail.",
    role: "Backend + dashboard",
    tech: ["AdonisJS", "Vue.js", "Crypto APIs", "REST"],
    accent: "violet",
    link: "https://ovypay.com",
  },
  {
    number: "02",
    title: "UITFX Admin, Partner & Client Portal",
    category: "Forex CRM / Partner Platform",
    description: "CRM portals for admin, partner and client operations.",
    problem: "Teams needed one place for partners, payouts and reports.",
    contribution: "CRM modules, dashboards, commission flows",
    result: "Partner activity, payouts and reports in one system.",
    role: "Full-stack features",
    tech: ["Laravel", "AdonisJS", "Vue.js", "ApexCharts"],
    accent: "cyan",
    link: "https://uitfx.com",
  },
];

const capabilities = [
  {
    index: "01",
    title: "Backend Systems",
    description: "APIs, business rules and secure service logic.",
    tools: "Laravel / AdonisJS / Node.js / REST / JWT",
  },
  {
    index: "02",
    title: "Product Interfaces",
    description: "Dashboards and workflows built for daily use.",
    tools: "Vue.js / Vuex / Vuetify / ApexCharts / Tailwind",
  },
  {
    index: "03",
    title: "Payments & Integrations",
    description: "Gateways, webhooks and traceable payment states.",
    tools: "Stripe / SSLCommerz / OvyPay / CheezyPay / G-Pay",
  },
  {
    index: "04",
    title: "Delivery & Operations",
    description: "Deployments, server setup and release workflow.",
    tools: "Linux / Nginx / PM2 / cPanel / Git",
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
    duration: "Aug 2023 - Present",
    location: "Dhaka, Bangladesh",
    summary:
      "Building CRM, partner and payment systems.",
    points: [
      "CRM and partner modules",
      "Crypto and card payment flows",
      "Releases and Linux operations",
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
      "Laravel and Vue application builds",
      "Database design and query improvement",
      "Payments, analytics and CRM integrations",
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

const normalizeProject = (doc, index) => {
  const data = doc.data();
  const fallback = defaultProjects[index % defaultProjects.length] || defaultProjects[0];
  const tech = Array.isArray(data.tech) && data.tech.length ? data.tech : fallback.tech;

  return {
    number: formatProjectNumber(data.number || data.order, index),
    title: data.title || fallback.title || "Portfolio Project",
    category: data.category || "Selected Work",
    description: data.description || "",
    problem: data.problem || fallback.problem || "",
    contribution: data.contribution || data.shipped || "",
    result: data.result || "",
    role: data.role || "",
    tech,
    accent: data.accent || fallback.accent || "violet",
    link: data.link || "#contact",
  };
};

const normalizeExperience = (doc) => {
  const data = doc.data();

  return {
    company: data.company || "",
    role: data.role || "",
    duration: data.duration || "",
    location: data.location || "",
    summary: data.summary || "",
    points: Array.isArray(data.points) ? data.points : [],
  };
};

const loadPortfolioContent = async () => {
  try {
    const [projectSnapshot, experienceSnapshot] = await Promise.all([
      getDocs(query(collection(db, "projects"), orderBy("order", "dsce"))),
      getDocs(query(collection(db, "experiences"), orderBy("order", "asc"))),
    ]);

    const firebaseProjects = projectSnapshot.docs.map(normalizeProject);
    const firebaseExperiences = experienceSnapshot.docs.map(normalizeExperience);

    if (firebaseProjects.length) {
      projects.value = firebaseProjects;
    }

    if (firebaseExperiences.length) {
      experiences.value = firebaseExperiences;
    }
  } catch (err) {
    console.error("Failed to load portfolio content from Firebase.", err);
  }
};

const closeMenu = () => {
  mobileMenuOpen.value = false;
};

const submitContact = async () => {
  success.value = "";
  error.value = "";

  const payload = {
    name: form.value.name.trim(),
    email: form.value.email.trim(),
    message: form.value.message.trim(),
  };

  if (!payload.name || !payload.email || !payload.message) {
    error.value = "Please complete all fields.";
    return;
  }

  try {
    loading.value = true;

    await addDoc(collection(db, "contacts"), {
      ...payload,
      createdAt: serverTimestamp(),
    });

    success.value = "Thank you. Your message has been sent.";
    form.value = { name: "", email: "", message: "" };
  } catch {
    error.value = "The message could not be sent. Please try again.";
  } finally {
    loading.value = false;
  }
};

onMounted(async () => {
  //await seedProjects();
  await loadPortfolioContent();
});
</script>

<template>
  <div class="site-shell">
    <div class="ambient ambient-one"></div>
    <div class="ambient ambient-two"></div>

    <header class="site-header">
      <nav class="navbar" aria-label="Primary navigation">
        <a class="brand" href="#top" aria-label="Amlan Kumar Mandol, home" @click="closeMenu">
          <img src="/akm.jpg" class="icon-image" alt="">
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
          <a href="#skills" @click="closeMenu">Skills</a>
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

          <p class="hero-kicker">Laravel, AdonisJS and Vue.js engineer</p>

          <h1>
            I build practical software
            <em>companies can trust.</em>
          </h1>

           
          <div class="profile-card" aria-label="Professional profile summary">
            <div class="profile-avatar">
              <img src="/akm.jpg" alt="akm">
            </div>
            <div class="profile-card-copy">
              <span>Full-Stack Software Engineer</span>
              <strong>Amlan Kumar Mandol</strong>
              <p>Laravel / AdonisJS / Node / Vue.js / React.js </p> <p>-- Dhaka, Bangladesh</p>
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

        <div class="hero-visual" aria-label="Application architecture overview">
          <div class="visual-frame">
            <div class="visual-topbar">
              <div class="visual-status">
                <span></span>
                SYSTEM ARCHITECTURE
              </div>
              <span>AK / 2026</span>
            </div>

            <div class="architecture">
              <div class="architecture-copy">
                <span class="architecture-label">Core focus</span>
                <h2>From interface to infrastructure.</h2>
                <p>
                  Frontend, backend and integrations working as one system.
                </p>
              </div>

              <img :src="heroVisual" alt="" />

            </div>

            <div class="visual-footer">
              <span>Vue.js</span>
              <span>Laravel</span>
              <span>AdonisJS</span>
              <span>MySQL</span>
            </div>
          </div>

          <div class="floating-note tech-note note-laravel">
            <span>Backend</span>
            Laravel
          </div>
          <div class="floating-note tech-note note-adonis">
            <span>API</span>
            AdonisJS
          </div>
          <div class="floating-note tech-note note-vue">
            <span>Frontend</span>
            Vue.js
          </div>
          <div class="floating-note tech-note note-mysql">
            <span>Database</span>
            MySQL
          </div>
        </div>
      </section>

      <div class="trust-strip" aria-label="Areas of expertise">
        <span>CRM Platforms</span>
        <i></i>
        <span>FinTech Workflows</span>
        <i></i>
        <span>Partner Systems</span>
        <i></i>
        <span>Payment Infrastructure</span>
        <i></i>
        <span>API Integrations</span>
      </div>

      <section id="about" class="section about-section">
        <div class="section-index">
          <span>01</span>
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

      <section id="skills" class="section skills-section">
        <div class="section-heading">
          <div class="section-index">
            <span>02</span>
            Toolbox
          </div>
          <div>
            <h2>Core tools I use to ship.</h2>
          </div>
        </div>

        <div class="skills-grid">
          <article v-for="group in skillGroups" :key="group.title" class="skill-card">
            <div class="skill-card-head">
              <img :src="group.logo" :alt="group.title" class="skill-logo" />
              <strong>{{ group.title }}</strong>
            </div>

            <div class="skill-list">
              <strong v-for="item in group.items" :key="item">{{ item }}</strong>
            </div>
          </article>
        </div>
      </section>

      <section id="projects" class="section projects-section">
        <div class="section-heading">
          <div class="section-index">
            <span>03</span>
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
              <div class="visual-toolbar">
                <span></span>
                <span></span>
                <span></span>
                <small>System overview</small>
              </div>
              <div class="visual-system">
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
                <span>What I shipped</span>
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

      <section id="experience" class="section experience-section">
        <div class="section-heading">
          <div class="section-index">
            <span>04</span>
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

      <section id="contact" class="contact-section">
        <div class="contact-intro">
          <div class="contact-label-row">
            <div class="section-index light">
              <span>05</span>
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
                  <path d="M6.6 10.8c1.4 2.8 3.8 5.2 6.6 6.6l2.2-2.2c.3-.3.8-.4 1.2-.3 1.3.4 2.6.6 4 .6.7 0 1.2.5 1.2 1.2v3.5c0 .7-.5 1.2-1.2 1.2C10.3 21.9 2.1 13.7 2.1 3.4c0-.7.5-1.2 1.2-1.2h3.5c.7 0 1.2.5 1.2 1.2 0 1.4.2 2.7.6 4 .1.4 0 .9-.3 1.2l-1.7 2.2Z" />
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
                  <path d="M4 5h16c1.1 0 2 .9 2 2v10c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V7c0-1.1.9-2 2-2Zm8 8.1L20 8V7.7l-8 5.1-8-5.1V8l8 5.1Z" />
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
        <img src="/akm.jpg" class="icon-image" alt="">
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
