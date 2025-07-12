<script setup lang="ts">
import SipeBlocks from './components/SipeBlocks.vue'
import IntroSection from './components/IntroSection.vue'
import FloatingCards from './components/FloatingCards.vue'
import Sponsors from './components/Sponsors.vue'
import CtaSection from './components/CtaSection.vue'
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

      <!-- Sponsors Section -->
      <section class="section sponsors-section">
        <Sponsors />
      </section>

      <!-- Floating Cards Section -->
      <section class="section cards-section">
        <FloatingCards />
      </section>

      <!-- CTA Section -->
      <section class="section cta-section">
        <CtaSection />
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
  color: #e2e8f0;
  background: #0a0a0f;
  overflow-x: hidden;
}

.app {
  min-height: 100vh;
  background: linear-gradient(180deg, #0a0a0f 0%, #0f0f23 50%, #1a1a2e 100%);
}

main {
  position: relative;
}

.section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  /* Initial state for animations - removed opacity: 0 to make sections visible by default */
}

.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.cards-section {
  padding: 4rem 2rem;
}

.sponsors-section {
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
  background: #1a1a2e;
}

::-webkit-scrollbar-thumb {
  background: #667eea;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #764ba2;
}

/* Responsive design */
@media (max-width: 1279px) {
  .section {
    min-height: auto;
    padding: 2rem 0;
  }
  
  .hero-section {
    min-height: 100vh;
    padding: 1rem;
  }
  
  .cards-section {
    padding: 3rem 1rem;
  }
  
  .sponsors-section {
    padding: 3rem 1rem;
  }
  
  /* Custom scrollbar for mobile */
  ::-webkit-scrollbar {
    width: 6px;
  }
}
</style>
