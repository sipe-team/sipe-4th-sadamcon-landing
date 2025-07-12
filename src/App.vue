<script setup lang="ts">
import SipeBlocks from './components/SipeBlocks.vue'
import IntroSection from './components/IntroSection.vue'
import FloatingCards from './components/FloatingCards.vue'
</script>

<template>
  <div class="app">
    <main>
      <!-- Hero Section with SIPE Blocks -->
      <section class="hero-section">
        <SipeBlocks />
      </section>

      <!-- Introduction Section -->
      <section class="section intro-section">
        <IntroSection />
      </section>

      <!-- Floating Cards Section -->
      <section class="section cards-section">
        <FloatingCards />
      </section>
    </main>
  </div>
</template>

<style>
@import url("https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.min.css");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  line-height: 1.6;
  color: #333;
  overflow-x: hidden;
}

.app {
  min-height: 100vh;
}

main {
  position: relative;
}

.section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  /* Initial state for animations - removed opacity: 0 to make sections visible by default */
}

.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  /* Remove background since SipeBlocks now handles it */
  position: relative;
  overflow: hidden;
}

.intro-section {
  background: #f8f9fa;
}

.cards-section {
  background: #ffffff;
  padding: 4rem 2rem;
}

/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}
</style>
