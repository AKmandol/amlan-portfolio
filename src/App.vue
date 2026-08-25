<script setup>
  import { ref } from "vue";
  import SkillImage from "./components/Skill.vue";
  import Header from "./components/Header.vue";
  import Hero from "./components/Hero.vue"
  import Project from "./components/Project.vue"
  import About from "./components/About.vue"
  import Experience from "./components/Experience.vue"
  import Contact from "./components/Contact.vue"
  import Footer from "./components/Footer.vue"
</script>

<template>
  <div class="site-shell">
    <div class="ambient ambient-one"></div>
    <div class="ambient ambient-two"></div>

    <Header />

    <main id="top">
      <Hero />
      <SkillImage />
      <Project />
      <About />
      <Experience />
      <Contact />
    </main>

    <Footer />

  </div>
</template>