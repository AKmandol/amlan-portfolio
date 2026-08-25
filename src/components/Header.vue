<script setup>
  import { ref } from "vue";
  const mobileMenuOpen = ref(false);
</script>

<template>
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
</template>
