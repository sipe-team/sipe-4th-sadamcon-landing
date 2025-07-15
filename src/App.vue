<script setup lang="ts">
import { useHead } from '@vueuse/head'
import SipeBlocks from './components/SipeBlocks.vue'
import IntroSection from './components/IntroSection.vue'
import FloatingCards from './components/FloatingCards.vue'
import Timetable from './components/Timetable.vue'
import Sponsors from './components/Sponsors.vue'
import CtaSection from './components/CtaSection.vue'

// SEO 최적화를 위한 동적 메타 태그 설정
useHead({
  htmlAttrs: {
    lang: 'ko',
  },
  meta: [
    { name: 'geo.region', content: 'KR' },
    { name: 'geo.country', content: 'KR' },
    { name: 'geo.placename', content: '대한민국' },
    { name: 'ICBM', content: '37.5665,126.9780' }, // 서울 좌표
    { name: 'application-name', content: 'SIPE 사담콘' },
    { name: 'msapplication-TileColor', content: '#2563eb' },
    { name: 'msapplication-config', content: '/browserconfig.xml' },
    { name: 'mobile-web-app-capable', content: 'yes' },
    { name: 'apple-mobile-web-app-capable', content: 'yes' },
    { name: 'apple-mobile-web-app-status-bar-style', content: 'default' },
    { name: 'apple-mobile-web-app-title', content: 'SIPE 사담콘' },
  ],
  link: [
    { rel: 'manifest', href: '/site.webmanifest' },
  ],
})
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

      <!-- Timetable Section -->
      <section class="section timetable-section">
        <Timetable />
      </section>

      <!-- CTA Section -->
      <section class="section cta-section">
        <CtaSection />
      </section>
    </main>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Pretendard Variable', 'Pretendard', 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Noto Sans KR', 'Malgun Gothic', 'Apple SD Gothic Neo', system-ui, sans-serif;
  line-height: 1.6;
  color: #e2e8f0;
  background: #0a0a0f;
  overflow-x: hidden;
  font-weight: 400;
  font-display: swap;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
}

/* Font weight definitions for better Android Chrome support */
.font-light { font-weight: 300 !important; }
.font-normal { font-weight: 400 !important; }
.font-medium { font-weight: 500 !important; }
.font-semibold { font-weight: 600 !important; }
.font-bold { font-weight: 700 !important; }
.font-extrabold { font-weight: 800 !important; }
.font-black { font-weight: 900 !important; }

/* Ensure font weights work on Android */
h1, h2, h3, h4, h5, h6 {
  font-weight: 700;
  font-family: inherit;
}

strong, b {
  font-weight: 700;
}

/* Force font loading and rendering */
* {
  font-feature-settings: "kern" 1;
  text-rendering: optimizeLegibility;
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
