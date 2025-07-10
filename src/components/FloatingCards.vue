<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const cardsRef = ref<HTMLElement>()
const cardElements = ref<HTMLElement[]>([])

interface Card {
  id: number
  title: string
  content: string
  image: string
  color: string
}

const cards: Card[] = [
  {
    id: 1,
    title: "Innovation",
    content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
    image: "https://images.unsplash.com/photo-1518709268805-4e9042af2176?w=400&h=300&fit=crop",
    color: "#667eea"
  },
  {
    id: 2,
    title: "Technology",
    content: "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
    image: "https://images.unsplash.com/photo-1518709594023-6eab9baa7959?w=400&h=300&fit=crop",
    color: "#764ba2"
  },
  {
    id: 3,
    title: "Design",
    content: "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
    image: "https://images.unsplash.com/photo-1518709286873-494fb702f4e4?w=400&h=300&fit=crop",
    color: "#f093fb"
  },
  {
    id: 4,
    title: "Development",
    content: "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
    image: "https://images.unsplash.com/photo-1518709268805-4e9042af2176?w=400&h=300&fit=crop",
    color: "#f5576c"
  }
]

onMounted(() => {
  console.log('FloatingCards mounted')
  
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        console.log('Cards intersection observed:', entry.isIntersecting)
        
        if (entry.isIntersecting) {
          console.log('Starting cards animations, cards count:', cardElements.value.length)
          
          // Animate cards with stagger
          if (cardElements.value.length > 0) {
            gsap.fromTo(cardElements.value,
              { 
                opacity: 0, 
                y: 100,
                scale: 0.8,
                rotation: -10
              },
              { 
                opacity: 1, 
                y: 0,
                scale: 1,
                rotation: 0,
                duration: 1.2,
                ease: "elastic.out(1, 0.3)",
                stagger: 0.2,
                onComplete: () => console.log('Cards initial animation complete')
              }
            )
            
            // Add floating animation to each card
            cardElements.value.forEach((card, index) => {
              if (card) {
                gsap.to(card, {
                  y: "random(-10, 10)",
                  rotation: "random(-2, 2)",
                  duration: "random(3, 5)",
                  repeat: -1,
                  yoyo: true,
                  ease: "sine.inOut",
                  delay: index * 0.5
                })
              }
            })
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

  if (cardsRef.value) {
    observer.observe(cardsRef.value)
    console.log('Observer attached to cards section')
  } else {
    console.error('CardsRef not found')
  }
})

const handleCardHover = (index: number, isHover: boolean) => {
  const card = cardElements.value[index]
  if (card) {
    gsap.to(card, {
      scale: isHover ? 1.05 : 1,
      y: isHover ? -10 : 0,
      duration: 0.3,
      ease: "power2.out"
    })
  }
}

const handleCardClick = (index: number) => {
  const card = cardElements.value[index]
  if (card) {
    gsap.to(card, {
      scale: 0.95,
      duration: 0.1,
      ease: "power2.out",
      onComplete: () => {
        gsap.to(card, {
          scale: 1.05,
          duration: 0.3,
          ease: "back.out(1.7)"
        })
      }
    })
  }
}
</script>

<template>
  <div ref="cardsRef" class="floating-cards">
    <div class="cards-header">
      <h2>발표 세션</h2>
      <p>여러분의 성장에 도움 한 스푼이 되어줄 발표들만 모아 봤어요</p>
    </div>
    
    <div class="cards-grid">
      <div
        v-for="(card, index) in cards"
        :key="card.id"
        :ref="el => cardElements[index] = el as HTMLElement"
        class="floating-card"
        :style="{ '--card-color': card.color }"
        @mouseenter="handleCardHover(index, true)"
        @mouseleave="handleCardHover(index, false)"
        @click="handleCardClick(index)"
      >
        <div class="card-image">
          <img :src="card.image" :alt="card.title" loading="lazy" />
          <div class="card-overlay"></div>
        </div>
        
        <div class="card-content">
          <h3 class="card-title">{{ card.title }}</h3>
          <p class="card-text">{{ card.content }}</p>
          <button class="card-button">
            Learn More
            <span class="arrow">→</span>
          </button>
        </div>
        
        <div class="card-glow"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.floating-cards {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.cards-header {
  text-align: center;
  margin-bottom: 4rem;
}

.cards-header h2 {
  font-size: 3rem;
  font-weight: 700;
  color: #333;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea, #764ba2);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.cards-header p {
  font-size: 1.2rem;
  color: #666;
  max-width: 600px;
  margin: 0 auto;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  perspective: 1000px;
}

.floating-card {
  position: relative;
  background: white;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  cursor: pointer;
  transition: all 0.3s ease;
  transform-style: preserve-3d;
  /* Ensure cards are visible initially */
  opacity: 1;
  transform: translateY(0) scale(1) rotate(0deg);
}

.floating-card:hover {
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.card-image {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.floating-card:hover .card-image img {
  transform: scale(1.1);
}

.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, var(--card-color, #667eea), transparent);
  opacity: 0.3;
  transition: opacity 0.3s ease;
}

.floating-card:hover .card-overlay {
  opacity: 0.5;
}

.card-content {
  padding: 2rem;
}

.card-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: #333;
  margin-bottom: 1rem;
}

.card-text {
  color: #666;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.card-button {
  background: linear-gradient(135deg, var(--card-color, #667eea), #764ba2);
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.card-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.arrow {
  transition: transform 0.3s ease;
}

.card-button:hover .arrow {
  transform: translateX(5px);
}

.card-glow {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, var(--card-color, #667eea) 0%, transparent 70%);
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  z-index: -1;
}

.floating-card:hover .card-glow {
  opacity: 0.1;
}

@media (max-width: 768px) {
  .cards-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .cards-header h2 {
    font-size: 2.5rem;
  }
  
  .cards-header p {
    font-size: 1rem;
  }
  
  .card-content {
    padding: 1.5rem;
  }
  
  .card-image {
    height: 150px;
  }
}
</style>
