<script setup>
import { ref } from "vue";
import { NCarousel, NImage, NImageGroup  } from "naive-ui";

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
    image: [
      "/project/forex1.png",
      "/project/forex2.png",
      "/project/forex3.avif",
    ],
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
    accent: "green",
    link: "https://ovypay.com",
    image: ["/project/ovy1.jpg", "/project/ovy2.avif"],
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
    accent: "orange",
    link: "https://tour.amlanbd.com",
    image: [
      "/project/tour1.avif",
      "/project/tour2.avif",
      "/project/tour3.avif",
    ],
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
    accent: "purple",
    link: "https://ecom.amlanbd.com",
    image: ["/project/ecom1.avif", "/project/ecom2.jpg", "/project/ecom3.avif"],
  },
];


const projects = ref(defaultProjects);
</script>

<style scoped></style>

<template>
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
      <article
        v-for="project in projects"
        :key="project.title"
        class="project-card"
        :class="`accent-${project.accent}`"
      >
        <!-- Top line -->
        <div class="project-topline">
          <div>
            <span class="project-number">
              {{ project.number }}
            </span>

            <span class="project-category">
              {{ project.category }}
            </span>
          </div>

          <span class="project-status">
            <i></i>
            Case study
          </span>
        </div>

        <!-- Project Image / Carousel -->
        <div class="project-visual">
          <div class="visual-system">
            <n-image-group>
              <n-carousel
                :show-arrow="true"
                :interval="2000"
                :effect="fade"
                style="width: 100%; height: 240px"
              >
                <n-image
                  v-for="(image, index) in project.image"
                  :key="index"
                  :src="image"
                  :alt="`Project visual ${index + 1}: ${project.title}`"
                  class="project-visual-img"
                  lazy
                />
              </n-carousel>
            </n-image-group>
          </div>
        </div>

        <!-- Project Description -->
        <div class="project-body">
          <h3>{{ project.title }}</h3>

          <p>
            {{ project.description }}
          </p>
        </div>

        <!-- Project Details -->
        <div class="project-proof">
          <div class="proof-item">
            <span>Problem</span>

            <strong>
              {{ project.problem }}
            </strong>
          </div>

          <div class="proof-item">
            <span>My role</span>

            <strong>
              {{ project.role }}
            </strong>
          </div>

          <div class="proof-item">
            <span>Shipped</span>

            <strong>
              {{ project.contribution }}
            </strong>
          </div>

          <div class="proof-item">
            <span>Result</span>

            <strong>
              {{ project.result }}
            </strong>
          </div>
        </div>

        <!-- Technologies + Link -->
        <div class="project-meta">
          <div class="tech-list">
            <span v-for="item in project.tech" :key="item">
              {{ item }}
            </span>
          </div>

          <a
            class="project-link"
            target="_blank"
            rel="noopener noreferrer"
            :href="project.link"
          >
            View project
          </a>
        </div>
      </article>
    </div>
  </section>
</template>
