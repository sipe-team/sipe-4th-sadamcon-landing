<script setup lang="ts">
import { onMounted, ref } from 'vue'

const sponsorsRef = ref<HTMLElement>()
const sponsorsGridRef = ref<HTMLElement>()

interface Sponsor {
  id: number
  name: string
  logo: string
  description?: string
}

const sponsors: Sponsor[] = [
  {
    id: 1,
    name: "dcamp",
    logo: "/img/sponsor_dcamp.svg",
  },
  {
    id: 2,
    name: "이벤터스",
    logo: "/img/sponsor_eventus.png",
  },
  {
    id: 3,
    name: "CLOOP",
    logo: "/img/sponsor_cloop.png",
  },
  {
    id: 4,
    name: "한빛미디어",
    logo: "/img/sponsor_hanbit.png",
  },
  {
    id: 5,
    name: "제이펍",
    logo: "/img/sponsor_jpub.png",
  },
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          if (sponsorsGridRef.value) {
            sponsorsGridRef.value.classList.add('animate-in')
          }
          observer.unobserve(entry.target)
        }
      })
    },
    { 
      threshold: 0.1,
      rootMargin: '0px 0px -50px 0px'
    }
  )

  if (sponsorsRef.value) {
    observer.observe(sponsorsRef.value)
  }
})
</script>

<template>
  <div ref="sponsorsRef" class="sponsors-section">
    <div class="sponsors-container">
      <div class="sponsors-header">
        <h2>후원사</h2>
        <p>SIPE 네 번째 사담콘과 함께해주시는 후원사를 소개합니다</p>
      </div>
      
      <div ref="sponsorsGridRef" class="sponsors-card">
        <div class="sponsors-grid">
          <div
            v-for="sponsor in sponsors"
            :key="sponsor.id"
            class="sponsor-item"
          >
            <div class="sponsor-logo">
              <img :src="sponsor.logo" :alt="sponsor.name" loading="lazy" />
            </div>
            <div class="sponsor-info">
              <h3 class="sponsor-name">{{ sponsor.name }}</h3>
              <p v-if="sponsor.description" class="sponsor-description">
                {{ sponsor.description }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.sponsors-section {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 4rem 2rem;
}

.sponsors-container {
  width: 100%;
}

.sponsors-header {
  text-align: center;
  margin-bottom: 4rem;
}

.sponsors-header h2 {
  font-size: 3rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea, #764ba2, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.sponsors-header p {
  font-size: 1.2rem;
  color: #b8c5d1;
  max-width: 600px;
  margin: 0 auto;
}

.sponsors-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 24px;
  padding: 3rem;
  box-shadow: 
    0 20px 50px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
  transition: transform 0.3s ease, opacity 0.3s ease;
  will-change: transform, opacity;
  transform: translate3d(0, 0, 0);
  
  /* Initial state for entrance animation */
  opacity: 0;
  transform: translate3d(0, 50px, 0) scale3d(0.95, 0.95, 1);
}

.sponsors-card.animate-in {
  opacity: 1;
  transform: translate3d(0, 0, 0) scale3d(1, 1, 1);
}

.sponsors-card:hover {
  transform: translate3d(0, -8px, 0);
}

.sponsors-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  align-items: center;
}

.sponsor-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  transition: transform 0.2s ease, opacity 0.2s ease;
  will-change: transform, opacity;
  transform: translate3d(0, 0, 0);
  position: relative;
}

.sponsor-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(255, 255, 255, 0.03);
  border-radius: 16px;
  opacity: 0;
  transition: opacity 0.2s ease;
  pointer-events: none;
}

.sponsor-item:hover {
  transform: translate3d(0, -4px, 0);
}

.sponsor-item:hover::before {
  opacity: 1;
}

.sponsor-logo {
  width: 120px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.5rem;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  padding: 1rem;
  transition: transform 0.2s ease;
  will-change: transform;
  transform: translate3d(0, 0, 0);
}

.sponsor-logo img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  transition: opacity 0.2s ease;
  will-change: opacity;
}

.sponsor-item:hover .sponsor-logo {
  transform: translate3d(0, 0, 0) scale(1.05);
}

.sponsor-item:hover .sponsor-logo img {
  opacity: 0.9;
}

.sponsor-info {
  width: 100%;
}

.sponsor-name {
  font-size: 1.3rem;
  font-weight: 600;
  color: #ffffff;
  margin-bottom: 0.5rem;
}

.sponsor-description {
  font-size: 1rem;
  color: #b8c5d1;
  line-height: 1.5;
}

@media (max-width: 1279px) {
  .sponsors-section {
    min-height: auto;
    padding: 3rem 1.5rem;
  }
  
  .sponsors-header {
    margin-bottom: 3rem;
  }
  
  .sponsors-header h2 {
    font-size: 2.5rem;
    margin-bottom: 0.875rem;
  }
  
  .sponsors-header p {
    font-size: 1rem;
    max-width: 500px;
  }
  
  .sponsors-card {
    padding: 2rem;
    border-radius: 20px;
  }
  
  .sponsors-grid {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
  }
  
  .sponsor-item {
    padding: 1.5rem;
    border-radius: 12px;
  }
  
  .sponsor-item::before {
    border-radius: 12px;
  }
  
  .sponsor-logo {
    width: 100px;
    height: 100px;
    margin-bottom: 1.25rem;
    border-radius: 12px;
  }
  
  .sponsor-name {
    font-size: 1.2rem;
    margin-bottom: 0.375rem;
  }
  
  .sponsor-description {
    font-size: 0.95rem;
  }
}

/* Mobile only - single column layout */
@media (max-width: 767px) {
  .sponsors-section {
    padding: 2rem 1rem;
  }
  
  .sponsors-header {
    margin-bottom: 2rem;
  }
  
  .sponsors-header h2 {
    font-size: 2rem;
  }
  
  .sponsors-header p {
    font-size: 0.9rem;
  }
  
  .sponsors-card {
    padding: 1.5rem;
  }
  
  .sponsors-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }
  
  .sponsor-item {
    padding: 1rem;
    border-radius: 12px;
  }
  
  .sponsor-item::before {
    border-radius: 12px;
  }
  
  .sponsor-logo {
    width: 80px;
    height: 80px;
    margin-bottom: 0.5rem;
    border-radius: 12px;
    padding: 0.75rem;
  }
  
  /* Show sponsor name with smaller font on mobile */
  .sponsor-info {
    display: block;
  }
  
  .sponsor-name {
    font-size: 0.8rem;
    margin-bottom: 0;
  }
  
  /* Hide sponsor description on mobile */
  .sponsor-description {
    display: none;
  }
}
</style>
