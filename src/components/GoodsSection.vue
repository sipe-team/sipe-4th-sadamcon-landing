<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref<HTMLElement>()
const titleRef = ref<HTMLElement>()
const descriptionRef = ref<HTMLElement>()
const goodsRefs = ref<HTMLElement[]>([])

interface GoodsItem {
  id: number
  name: string
  image: string | string[]
  color: string
}

const goodsItems: GoodsItem[] = [
  {
    id: 1,
    name: 'SIPE 테크 미니 파우치',
    image: ['/img/goods_pouch_1.png', '/img/goods_pouch_2.png'],
    color: '#667eea'
  },
  {
    id: 2,
    name: 'SIPE 양우산',
    image: '/img/goods_umbrella.png',
    color: '#764ba2'
  },
  {
    id: 3,
    name: 'SIPE 키캡 스티커',
    image: '/img/goods_sticker.png',
    color: '#a8edea'
  }
]

onMounted(() => {
  if (!sectionRef.value || !titleRef.value || !descriptionRef.value) return

  // Title animation
  gsap.fromTo(titleRef.value, 
    {
      opacity: 0,
      y: 50
    },
    {
      opacity: 1,
      y: 0,
      duration: 1.2,
      ease: "power3.out",
      scrollTrigger: {
        trigger: sectionRef.value,
        start: "top 80%",
        end: "top 20%",
        toggleActions: "play none none reverse"
      }
    }
  )

  // Description animation
  gsap.fromTo(descriptionRef.value, 
    {
      opacity: 0,
      y: 30
    },
    {
      opacity: 0.9,
      y: 0,
      duration: 1,
      ease: "power3.out",
      delay: 0.3,
      scrollTrigger: {
        trigger: sectionRef.value,
        start: "top 80%",
        end: "top 20%",
        toggleActions: "play none none reverse"
      }
    }
  )

  // Goods items animation
  goodsRefs.value.forEach((ref, index) => {
    if (!ref) return
    
    gsap.fromTo(ref,
      {
        opacity: 0,
        y: 50,
        scale: 0.8,
        rotationY: 45
      },
      {
        opacity: 1,
        y: 0,
        scale: 1,
        rotationY: 0,
        duration: 1.5,
        ease: "power3.out",
        delay: index * 0.2,
        scrollTrigger: {
          trigger: ref,
          start: "top 85%",
          end: "top 15%",
          toggleActions: "play none none reverse"
        }
      }
    )

    // Floating animation
    gsap.to(ref, {
      y: "random(-5, 5)",
      x: "random(-5, 5)",
      rotation: "random(-5, 5)",
      duration: "random(3, 5)",
      ease: "sine.inOut",
      repeat: -1,
      yoyo: true,
      delay: index * 0.5
    })
  })
})
</script>

<template>
  <div ref="sectionRef" class="goods-section">
    <div class="goods-container">
      <!-- Background decorative elements -->
      <div class="background-blur blur-1"></div>
      <div class="background-blur blur-2"></div>
      <div class="background-blur blur-3"></div>
      
      <!-- Title -->
      <h2 ref="titleRef" class="goods-title">
        <span class="title-gradient">사담콘 굿즈 소개</span>
      </h2>
      
      <!-- Description -->
      <p ref="descriptionRef" class="goods-description">
        사담콘에 참여하는 모든 분들께 아래 기념품을 드립니다
      </p>
      
      <!-- Goods Grid -->
      <div class="goods-grid">
        <div 
          v-for="(item, index) in goodsItems"
          :key="item.id"
          :ref="(el) => goodsRefs[index] = el as HTMLElement"
          class="goods-item"
          :style="{ '--item-color': item.color }"
        >
          <div class="goods-card">
            <div class="goods-image-container">
              <!-- Multiple images for pouch -->
              <template v-if="Array.isArray(item.image)">
                <div class="pouch-images">
                  <img 
                    v-for="(img, imgIndex) in item.image"
                    :key="imgIndex"
                    :src="img" 
                    :alt="`${item.name} ${imgIndex + 1}`"
                    class="goods-image pouch-image"
                    :class="`pouch-${imgIndex + 1}`"
                  />
                </div>
              </template>
              <!-- Single image for other items -->
              <template v-else>
                <img 
                  :src="item.image" 
                  :alt="item.name"
                  class="goods-image"
                />
              </template>
              <div class="image-glow"></div>
            </div>
            <div class="goods-info">
              <span class="goods-number">{{ item.id }}.</span>
              <h3 class="goods-name">{{ item.name }}</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.goods-section {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 6rem 2rem;
  overflow: hidden;
}

.goods-container {
  position: relative;
  max-width: 1400px;
  width: 100%;
  z-index: 2;
}

/* Background decorative elements */
.background-blur {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  opacity: 0.3;
  pointer-events: none;
}

.blur-1 {
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, #667eea 0%, transparent 70%);
  top: 10%;
  left: -10%;
  animation: float 15s ease-in-out infinite;
}

.blur-2 {
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, #764ba2 0%, transparent 70%);
  top: 60%;
  right: -5%;
  animation: float 12s ease-in-out infinite reverse;
}

.blur-3 {
  width: 350px;
  height: 350px;
  background: radial-gradient(circle, #a8edea 0%, transparent 70%);
  bottom: 20%;
  left: 20%;
  animation: float 18s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translate(0, 0) rotate(0deg); }
  25% { transform: translate(20px, -30px) rotate(5deg); }
  50% { transform: translate(-15px, -20px) rotate(-3deg); }
  75% { transform: translate(25px, -10px) rotate(7deg); }
}

/* Title */
.goods-title {
  text-align: center;
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 800;
  margin-bottom: 1.5rem;
  opacity: 0;
}

.title-gradient {
  background: linear-gradient(135deg, #667eea, #764ba2, #a8edea);
  background-size: 300% 300%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradientShift 6s ease-in-out infinite;
}

/* Description */
.goods-description {
  text-align: center;
  font-size: clamp(1.1rem, 2.5vw, 1.3rem);
  font-weight: 400;
  color: #a1a1aa;
  margin-bottom: 4rem;
  line-height: 1.6;
  opacity: 0;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

/* Goods Grid */
.goods-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 3rem;
  max-width: 1200px;
  margin: 0 auto;
}

.goods-item {
  opacity: 0;
  perspective: 1000px;
}

.goods-card {
  position: relative;
  background: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 24px;
  padding: 2.5rem;
  transition: all 0.4s cubic-bezier(0.25, 0.8, 0.25, 1);
  overflow: hidden;
  cursor: pointer;
}

.goods-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, var(--item-color, #667eea) 0%, transparent 50%);
  opacity: 0.1;
  transition: opacity 0.4s ease;
  pointer-events: none;
}

.goods-card:hover {
  transform: translateY(-10px) scale(1.02);
  border-color: rgba(255, 255, 255, 0.2);
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.3),
    0 0 80px rgba(var(--item-color), 0.2);
}

.goods-card:hover::before {
  opacity: 0.2;
}

/* Image Container */
.goods-image-container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 200px;
  margin-bottom: 2rem;
  overflow: hidden;
}

.pouch-images {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
}

.goods-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  filter: drop-shadow(0 10px 20px rgba(0, 0, 0, 0.3));
  transition: all 0.4s ease;
  z-index: 2;
  position: relative;
}

.pouch-image {
  position: absolute;
  max-width: 85%;
  max-height: 85%;
}

.pouch-1 {
  transform: translateX(-15px) translateY(-10px) rotate(-8deg);
  z-index: 3;
}

.pouch-2 {
  transform: translateX(15px) translateY(10px) rotate(8deg);
  z-index: 2;
}

.goods-card:hover .pouch-1 {
  transform: translateX(-20px) translateY(-15px) rotate(-12deg) scale(1.05);
}

.goods-card:hover .pouch-2 {
  transform: translateX(20px) translateY(15px) rotate(12deg) scale(1.05);
}

.goods-card:hover .goods-image:not(.pouch-image) {
  transform: scale(1.1) rotateY(10deg);
  filter: drop-shadow(0 15px 30px rgba(0, 0, 0, 0.4));
}

.image-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 80%;
  height: 80%;
  background: radial-gradient(circle, var(--item-color, #667eea) 0%, transparent 70%);
  transform: translate(-50%, -50%);
  opacity: 0.3;
  filter: blur(30px);
  transition: all 0.4s ease;
  z-index: 1;
}

.goods-card:hover .image-glow {
  opacity: 0.5;
  transform: translate(-50%, -50%) scale(1.2);
}

/* Goods Info */
.goods-info {
  text-align: center;
}

.goods-number {
  display: inline-block;
  font-size: 1.2rem;
  font-weight: 700;
  color: var(--item-color, #667eea);
  margin-bottom: 0.5rem;
  opacity: 0.8;
}

.goods-name {
  font-size: 1.4rem;
  font-weight: 600;
  color: #e2e8f0;
  line-height: 1.3;
  margin: 0;
}

/* Responsive Design */
@media (max-width: 1279px) {
  .goods-section {
    padding: 4rem 1rem;
  }
  
  .goods-grid {
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }
  
  .goods-card {
    padding: 2rem;
  }
  
  .goods-image-container {
    height: 160px;
    margin-bottom: 1.5rem;
  }
}

@media (max-width: 767px) {
  .goods-section {
    padding: 3rem 1rem;
  }
  
  .goods-title {
    margin-bottom: 1rem;
  }
  
  .goods-description {
    margin-bottom: 3rem;
  }
  
  .goods-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .goods-card {
    padding: 1.5rem;
  }
  
  .goods-image-container {
    height: 140px;
    margin-bottom: 1rem;
  }
  
  .goods-name {
    font-size: 1.2rem;
  }
  
  .background-blur {
    display: none;
  }
}
</style>
