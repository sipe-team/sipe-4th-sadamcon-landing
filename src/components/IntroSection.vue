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
            사담콘은 사이퍼들의 이야기(談)를 나누는 컨퍼런스로, 다양한 분야에 종사하는 현직 개발자들이 경험과 인사이트를 공유하는 행사입니다.
          </p>
          
          <div class="sipe-info-card">
            <h3>SIPE는 어떤 동아리인가요?</h3>
            <p>
              <strong>SIPE</strong>는 <em>Sharing Insights with People Everyday</em>의 약자입니다.
            </p>
            <p>
              현직 개발자들이 함께 교류하며 성장하는 IT 커뮤니티를 지향하고 있습니다.
            </p>
            <p>
              1기에서부터 4기까지 총 <strong>131명의 사이퍼(SIPER)</strong>들이 함께하고 있으며, 온/오프라인에서 활발하게 활동하고 있습니다.
            </p>
            <div class="sipe-link">
              SIPE에 대해 더 궁금하시다면? 
              <a href="https://sipe.team/" target="_blank" rel="noopener noreferrer">sipe.team</a>
            </div>
          </div>

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
  justify-content: center;
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

.sipe-info-card {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 20px;
  padding: 2rem;
  margin: 2rem 0;
  box-shadow: 
    0 8px 32px rgba(0, 0, 0, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  will-change: transform;
  transform: translateZ(0);
}

.sipe-info-card:hover {
  background: rgba(255, 255, 255, 0.12);
  border-color: rgba(255, 255, 255, 0.2);
  transform: translate3d(0, -2px, 0);
  box-shadow: 
    0 12px 40px rgba(0, 0, 0, 0.25),
    inset 0 1px 0 rgba(255, 255, 255, 0.25);
}

.sipe-info-card h3 {
  color: #ffffff;
  font-size: 1.3rem;
  font-weight: 600;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.sipe-info-card p {
  color: #b8c5d1;
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.sipe-info-card p:last-of-type {
  margin-bottom: 1.5rem;
}

.sipe-info-card strong {
  color: #ffffff;
  font-weight: 600;
}

.sipe-info-card em {
  color: #a8edea;
  font-style: italic;
}

.sipe-link {
  color: #b8c5d1;
  font-size: 0.95rem;
}

.sipe-link a {
  color: #667eea;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s ease;
}

.sipe-link a:hover {
  color: #a8edea;
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

@media (max-width: 1279px) {
  .container {
    grid-template-columns: 1fr;
    gap: 2rem;
    padding: 1.5rem;
  }
  
  .intro-content {
    padding-right: 0;
    text-align: center;
  }
  
  .intro-title {
    font-size: 2.5rem;
    margin-bottom: 1.5rem;
  }
  
  .intro-text {
    font-size: 1rem;
  }
  
  .sipe-info-card {
    padding: 1.5rem;
    margin: 1.5rem 0;
  }
  
  .sipe-info-card h3 {
    font-size: 1.2rem;
  }
  
  .sipe-info-card p {
    font-size: 0.95rem;
  }
  
  .cta-button {
    padding: 0.875rem 1.75rem;
    font-size: 1rem;
  }
  
  .intro-visual {
    height: 200px;
  }
  
  .floating-shape {
    opacity: 0.08;
  }
  
  .shape-1 {
    width: 80px;
    height: 80px;
  }
  
  .shape-2 {
    width: 60px;
    height: 60px;
  }
  
  .shape-3 {
    width: 70px;
    height: 70px;
  }
}
</style>
