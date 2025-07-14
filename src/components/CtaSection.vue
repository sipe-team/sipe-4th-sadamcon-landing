<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const ctaSectionRef = ref<HTMLElement>()
const ctaTitleRef = ref<HTMLElement>()
const ctaContentRef = ref<HTMLElement>()

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
          if (ctaTitleRef.value) {
            gsap.fromTo(ctaTitleRef.value,
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
          if (ctaContentRef.value) {
            gsap.fromTo(ctaContentRef.value,
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

  if (ctaSectionRef.value) {
    observer.observe(ctaSectionRef.value)
  }
})
</script>

<template>
  <div ref="ctaSectionRef" class="cta-section">
    <div class="cta-container">
      <div class="cta-content">
        <h2 ref="ctaTitleRef" class="cta-title">
          지금 신청하세요
        </h2>
        <div ref="ctaContentRef" class="cta-text">
          <p class="cta-description">
            SIPE 네 번째 사담콘에서 현직 개발자들의 생생한 경험과 인사이트를 만나보세요.
          </p>
          <p class="cta-subtitle">
            여러분의 성장을 위한 소중한 시간이 될 거에요!
          </p>
          
          <div class="cta-highlight-card">
            <div class="highlight-item">
              <div class="highlight-icon">📅</div>
              <div class="highlight-text">
                <h4>일정</h4>
                <p>2025년 8월 2일 토요일 13:30 - 18:00</p>
              </div>
            </div>
            <div class="highlight-item">
              <div class="highlight-icon">📍</div>
              <div class="highlight-text">
                <h4>장소</h4>
                <p>서울 마포구 마포대로 122, 프론트원 5층 박병원홀</p>
              </div>
            </div>
            <div class="highlight-item">
              <div class="highlight-icon">👥</div>
              <div class="highlight-text">
                <h4>모집 정원</h4>
                <p>180명</p>
              </div>
            </div>
          </div>

          <div class="cta-action">
            <button class="cta-button" @click="handleRegister">
              지금 신청하기
              <span class="button-icon">→</span>
            </button>
            <p class="cta-note">
              * 티켓은 선착순으로 마감될 수 있습니다.
            </p>
          </div>
        </div>
      </div>
      
      <div class="cta-visual">
        <div class="floating-element element-1"></div>
        <div class="floating-element element-2"></div>
        <div class="floating-element element-3"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cta-section {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 4rem 2rem;
}

.cta-container {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.cta-content {
  padding-right: 2rem;
}

.cta-title {
  font-size: 4rem;
  font-weight: 900;
  color: #ffffff;
  margin-bottom: 2rem;
  line-height: 1.1;
  background: linear-gradient(135deg, #667eea, #764ba2, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  /* Ensure title is visible initially */
  opacity: 1;
  transform: translateY(0);
}

.cta-text {
  /* Ensure content is visible initially */
  opacity: 1;
  transform: translateY(0);
}

.cta-description {
  font-size: 1.3rem;
  line-height: 1.7;
  color: #e2e8f0;
  margin-bottom: 1rem;
  font-weight: 500;
}

.cta-subtitle {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #b8c5d1;
  margin-bottom: 3rem;
}

.cta-highlight-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  margin-bottom: 3rem;
  box-shadow: 
    0 10px 40px rgba(0, 0, 0, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  will-change: transform;
  transform: translateZ(0);
  text-align: left;
}

.cta-highlight-card:hover {
  background: rgba(255, 255, 255, 0.08);
  border-color: rgba(255, 255, 255, 0.15);
  transform: translate3d(0, -4px, 0);
  box-shadow: 
    0 15px 50px rgba(0, 0, 0, 0.25),
    inset 0 1px 0 rgba(255, 255, 255, 0.15);
}

.highlight-item {
  display: flex;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 1.5rem;
}

.highlight-item:last-child {
  margin-bottom: 0;
}

.highlight-icon {
  font-size: 2rem;
  width: 60px;
  height: 60px;
  display: flex;
  flex-shrink: 0;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.highlight-text h4 {
  color: #ffffff;
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.highlight-text p {
  color: #b8c5d1;
  font-size: 1rem;
}

.cta-action {
  text-align: center;
}

.cta-button {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #ffffff;
  padding: 1.25rem 3rem;
  font-size: 1.2rem;
  font-weight: 700;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  box-shadow: 
    0 10px 40px rgba(0, 0, 0, 0.3),
    0 5px 20px rgba(0, 0, 0, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.3),
    inset 0 -1px 0 rgba(0, 0, 0, 0.2);
  position: relative;
  overflow: hidden;
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1.5rem;
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
  transform: translateY(-4px);
  background: rgba(255, 255, 255, 0.12);
  border: 1px solid rgba(255, 255, 255, 0.3);
  box-shadow: 
    0 15px 50px rgba(0, 0, 0, 0.4),
    0 8px 25px rgba(0, 0, 0, 0.25),
    inset 0 1px 0 rgba(255, 255, 255, 0.4),
    inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}

.cta-button:hover::before {
  left: 100%;
}

.cta-button:hover .button-icon {
  transform: translateX(5px);
}

.cta-button:active {
  transform: translateY(-2px);
  box-shadow: 
    0 8px 30px rgba(0, 0, 0, 0.35),
    0 4px 15px rgba(0, 0, 0, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.25),
    inset 0 -1px 0 rgba(0, 0, 0, 0.3);
}

.button-icon {
  transition: transform 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  font-size: 1.3rem;
}

.cta-note {
  color: #a0aec0;
  font-size: 0.9rem;
  font-style: italic;
}

.cta-visual {
  position: relative;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.floating-element {
  position: absolute;
  border-radius: 20px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  opacity: 0.1;
}

.element-1 {
  width: 150px;
  height: 150px;
  top: 10%;
  left: 10%;
  animation: float1 8s ease-in-out infinite;
  border-radius: 50%;
}

.element-2 {
  width: 100px;
  height: 100px;
  top: 60%;
  right: 20%;
  animation: float2 6s ease-in-out infinite;
  transform: rotate(45deg);
}

.element-3 {
  width: 120px;
  height: 120px;
  bottom: 15%;
  left: 40%;
  animation: float3 7s ease-in-out infinite;
  border-radius: 30px;
}

@keyframes float1 {
  0%, 100% { transform: translateY(0px) scale(1); }
  50% { transform: translateY(-30px) scale(1.1); }
}

@keyframes float2 {
  0%, 100% { transform: rotate(45deg) translateY(0px); }
  50% { transform: rotate(50deg) translateY(-25px); }
}

@keyframes float3 {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-35px) rotate(5deg); }
}

@media (max-width: 1279px) {
  .cta-section {
    min-height: auto;
    padding: 4rem 1.5rem;
  }
  
  .cta-container {
    grid-template-columns: 1fr;
    gap: 3rem;
  }
  
  .cta-content {
    padding-right: 0;
    text-align: center;
  }
  
  .cta-title {
    font-size: 3rem;
    margin-bottom: 1.5rem;
  }
  
  .cta-description {
    font-size: 1.1rem;
    margin-bottom: 0.875rem;
  }
  
  .cta-subtitle {
    font-size: 1rem;
    margin-bottom: 2.5rem;
  }
  
  .cta-highlight-card {
    padding: 1.5rem;
    margin-bottom: 2.5rem;
  }
  
  .highlight-item {
    gap: 1rem;
    margin-bottom: 1.25rem;
  }
  
  .highlight-icon {
    width: 50px;
    height: 50px;
    font-size: 1.75rem;
  }
  
  .highlight-text h4 {
    font-size: 1rem;
  }
  
  .highlight-text p {
    font-size: 0.95rem;
  }
  
  .cta-button {
    padding: 1rem 2.5rem;
    font-size: 1.1rem;
    margin-bottom: 1.25rem;
  }
  
  .cta-note {
    font-size: 0.85rem;
  }
  
  .cta-visual {
    height: 300px;
  }
  
  .floating-element {
    opacity: 0.06;
  }
  
  .element-1 {
    width: 100px;
    height: 100px;
  }
  
  .element-2 {
    width: 70px;
    height: 70px;
  }
  
  .element-3 {
    width: 80px;
    height: 80px;
  }
}
</style>
