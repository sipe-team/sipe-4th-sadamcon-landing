<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const introRef = ref<HTMLElement>()
const titleRef = ref<HTMLElement>()
const contentRef = ref<HTMLElement>()

const handleRegister = () => {
  const url = new URL('https://event-us.kr/sipe/event/104609')
  
  // Get UTM parameters from the URL
  const utmSource = new URLSearchParams(window.location.search).get('utm_source')
  const utmMedium = new URLSearchParams(window.location.search).get('utm_medium')
  const utmCampaign = new URLSearchParams(window.location.search).get('utm_campaign')
  if (utmSource && utmMedium && utmCampaign) {
    url.searchParams.set('utm_source', utmSource)
    url.searchParams.set('utm_medium', utmMedium)
    url.searchParams.set('utm_campaign', utmCampaign)
  } else {
    // Default UTM parameters if not present
    url.searchParams.set('utm_source', 'landing')
    url.searchParams.set('utm_medium', 'web')
    url.searchParams.set('utm_campaign', 'mlt0tcndtl')
  }

  window.open(url.toString(), '_blank')
}

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          // Animate title
          if (titleRef.value) {
            gsap.fromTo(titleRef.value,
              { opacity: 0, y: 50 },
              { 
                opacity: 1, 
                y: 0, 
                duration: 1, 
                ease: "power2.out",
              }
            )
          }
          
          // Animate content with delay
          if (contentRef.value) {
            gsap.fromTo(contentRef.value,
              { opacity: 0, y: 30 },
              { 
                opacity: 1, 
                y: 0, 
                duration: 1, 
                delay: 0.3, 
                ease: "power2.out",
              }
            )
          }
          
          observer.unobserve(entry.target)
        }
      })
    },
    { 
      threshold: 0.1,
      rootMargin: '0px 0px -100px 0px'
    }
  )

  if (introRef.value) {
    observer.observe(introRef.value)
  } else {
    console.error('IntroRef not found')
  }
})
</script>

<template>
  <div ref="introRef" class="intro-section">
    <div class="container">
      <div class="intro-content">
        <h2 ref="titleRef" class="intro-title">
          SIPE 네 번째 사담콘
        </h2>
        <div ref="contentRef" class="intro-text">
          <p>
            네 번째 사담콘은 SIPE의 개발자 컨퍼런스로, 개발자들이 모여 서로의 경험과 지식을 나누는 자리입니다. 이번 사담콘에서는 다양한 주제의 발표 세션과 네트워킹 이벤트가 준비되어 있습니다.
          </p>
          <p>
            Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu 
            fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in 
            culpa qui officia deserunt mollit anim id est laborum.
          </p>
          <p>
            Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque 
            laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi 
            architecto beatae vitae dicta sunt explicabo.
          </p>
          <div class="cta-section">
            <button class="cta-button" @click="handleRegister">
              지금 신청하기
            </button>
          </div>
        </div>
      </div>
      <div class="intro-visual">
        <div class="floating-shape shape-1"></div>
        <div class="floating-shape shape-2"></div>
        <div class="floating-shape shape-3"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.intro-section {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  padding: 2rem;
}

.intro-content {
  padding-right: 2rem;
}

.intro-title {
  font-size: 3.5rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 2rem;
  line-height: 1.2;
  background: linear-gradient(135deg, #667eea, #764ba2, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  /* Ensure title is visible initially */
  opacity: 1;
  transform: translateY(0);
}

.intro-text {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #b8c5d1;
  /* Ensure content is visible initially */
  opacity: 1;
  transform: translateY(0);
}

.intro-text p {
  margin-bottom: 1.5rem;
}

.cta-section {
  margin-top: 2.5rem;
}

.cta-button {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #ffffff;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  box-shadow: 
    0 8px 32px rgba(0, 0, 0, 0.3),
    0 4px 16px rgba(0, 0, 0, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.3),
    inset 0 -1px 0 rgba(0, 0, 0, 0.2);
  position: relative;
  overflow: hidden;
}

.cta-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.4),
    transparent
  );
  transition: left 0.6s ease;
}

.cta-button:hover {
  transform: translateY(-3px);
  background: rgba(255, 255, 255, 0.12);
  border: 1px solid rgba(255, 255, 255, 0.3);
  box-shadow: 
    0 12px 40px rgba(0, 0, 0, 0.4),
    0 6px 20px rgba(0, 0, 0, 0.25),
    inset 0 1px 0 rgba(255, 255, 255, 0.4),
    inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}

.cta-button:hover::before {
  left: 100%;
}

.cta-button:active {
  transform: translateY(-1px);
  box-shadow: 
    0 6px 24px rgba(0, 0, 0, 0.35),
    0 3px 12px rgba(0, 0, 0, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.25),
    inset 0 -1px 0 rgba(0, 0, 0, 0.3);
}

.intro-visual {
  position: relative;
  height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.floating-shape {
  position: absolute;
  border-radius: 20px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  opacity: 0.15;
}

.shape-1 {
  width: 120px;
  height: 120px;
  top: 20%;
  left: 20%;
  animation: float-1 6s ease-in-out infinite;
}

.shape-2 {
  width: 80px;
  height: 80px;
  top: 60%;
  right: 30%;
  animation: float-2 8s ease-in-out infinite;
  border-radius: 50%;
}

.shape-3 {
  width: 100px;
  height: 100px;
  bottom: 20%;
  left: 60%;
  animation: float-3 7s ease-in-out infinite;
  transform: rotate(45deg);
}

@keyframes float-1 {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(10deg); }
}

@keyframes float-2 {
  0%, 100% { transform: translateY(0px) scale(1); }
  50% { transform: translateY(-30px) scale(1.1); }
}

@keyframes float-3 {
  0%, 100% { transform: rotate(45deg) translateY(0px); }
  50% { transform: rotate(55deg) translateY(-25px); }
}

@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .intro-content {
    padding-right: 0;
    text-align: center;
  }
  
  .intro-title {
    font-size: 2.5rem;
  }
  
  .intro-text {
    font-size: 1rem;
  }
  
  .intro-visual {
    height: 200px;
  }
  
  .floating-shape {
    opacity: 0.05;
  }
}
</style>
