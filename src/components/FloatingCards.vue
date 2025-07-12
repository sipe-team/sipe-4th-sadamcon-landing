<script setup lang="ts">
import { onMounted, ref } from 'vue'

const cardsRef = ref<HTMLElement>()
const cardElements = ref<HTMLElement[]>([])
const selectedCard = ref<Card | null>(null)
const isModalOpen = ref(false)

interface Card {
  id: number
  title: string
  content: string
  speakerName: string
  speakerIntro: string
  image: string
  color: string
  linkedinUrl?: string
}

const cards: Card[] = [
  {
    id: 0,
    title: "KEYNOTE",
    content: "SIPE 소개 및 행사 안내",
    speakerName: "심미진",
    speakerIntro: `안녕하세요, 프론트엔드 주니어 개발자 심미진입니다. IT 커뮤니티 활동하는 것을 좋아하고, 경험하고 얻은 것들을 다함께 공유함으로써 IT 생태계에 조금이라도 기여하고자 합니다.`,
    image: "/img/profile_mijin.png",
    color: "#667eea",
    linkedinUrl: 'https://www.linkedin.com/in/jun-hwan-jang-aa7567209/',
  },
  {
    id: 1,
    title: "Redis Lettuce 기반 분산 락으로 데이터 정합성 보장하기",
    content: "Redis Lettuce 기반 분산 락을 통해 주문·결제 등에서 발생할 수 있는 중복 처리 문제를 해결하고, 동시성 환경에서도 데이터 정합성을 보장하는 구조와 실제 적용 사례를 소개합니다. 또한 락 해제의 한계와 향후 개선 방향까지 함께 다룹니다.",
    speakerName: "장준환",
    speakerIntro: `SI, 메시징 그리고 라스트마일을 거쳐, 
현재는 이커머스 플랫폼에서 
더 나은 서비스를 제공하기 위해 항상 고민하고 있습니다.

JVM 생태계와 데이터 엔지니어링에 큰 매력을 느끼고 있습니다.`,
    image: "https://s.abcnews.com/images/Business/GTY_steve_jobs_2_jtm_150323.jpg",
    color: "#667eea",
    linkedinUrl: 'https://www.linkedin.com/in/jun-hwan-jang-aa7567209/',
  },
  {
    id: 2,
    title: "현업에서의 LLMOps",
    content: "현업에서의 경험을 바탕으로 LLMOps 워크플로우 전반—데이터 준비, 모델 운영, 모니터링 등—에서 실제로 어떤 작업이 이루어지는지 설명합니다. 또한 다양한 LLMOps 도구들을 소개하며 실무에 적용할 수 있는 방안들을 함께 제시합니다.",
    speakerName: "김민준",
    speakerIntro: `한국 대기업 문화를 가진 IT 기업부터, 실리콘밸리 문화의 금융 에이전트 스타트업까지 다양한 경험을 쌓은 소프트웨어 엔지니어 김민준입니다.`,
    image: "/img/profile_minjun.jpg",
    color: "#764ba2",
    linkedinUrl: 'https://www.linkedin.com/in/neilkim404/',
  },
  {
    id: 3,
    title: "지구 반대편을 대응하는 어플리케이션을 위해",
    content: "글로벌 서비스를 운영하며 겪은 다국어, 현지 정책, UI 분기 등의 어려움을 주니어 개발자의 시각으로 풀어낸 경험을 공유합니다. 지구 반대편 사용자도 자연스럽게 사용할 수 있는 서비스를 만들기 위해 고민한 실질적인 방법들을 소개합니다.",
    speakerName: "김민규",
    speakerIntro: `자동차도 없고, 면허도 없지만, 전기차 도메인에서 일하고 있는 프론트엔드 개발자 김민규입니다.
프론트엔드 이외에도 홈서버나 인프라, 3D 프린트, 그리고 맥주에도 관심이 많아요.`,
    image: "/img/profile_minkyu.webp",
    color: "#f093fb"
  },
  {
    id: 4,
    title: "알잘딱 에이전트 만들기: Context Engineering",
    content: "행위 중심의 에이전트를 효과적으로 만들기 위해선 LLM의 한계를 극복할 수 있는 정교한 Context Engineering이 핵심이며, 이를 위해 LangChain/LangGraph 같은 도구들이 활용됩니다. 또한 에이전트의 품질을 평가할 수 있는 지표 없이 실서비스에 안정적으로 적용하기 어렵다는 점도 강조합니다.",
    speakerName: "조혜정",
    speakerIntro: `안녕하세요. AI Research Engineer 조혜정입니다.
버티컬 도메인 에이전트를 연구/개발하며, 컨텍스트 엔지니어링을 통해 성능을 고도화하는 작업을 담당해 왔습니다.
이번 사담콘 에서는 그 과정에서 얻은 인사이트와 실무 노하우를 공유하고자 합니다 :)`,
    image: "/img/profile_hyejeong.jpeg",
    color: "#f5576c",
    linkedinUrl: 'https://www.linkedin.com/in/hyejeong-jo-1069b2235/'
  },
  {
    id: 5,
    title: "디자이너 출신 개발자의 PM 도전기",
    content: "디자인 전공 후 프론트엔드 개발자로 일하다가 PM 인턴으로 커리어를 확장하게 된 개인적인 여정과 동기를 공유합니다. 개발자에서 PM으로 전환하기까지의 준비 과정과 실제 경험을 솔직하게 들려드립니다.",
    speakerName: "이지원",
    speakerIntro: `안녕하세요, 이지원입니다.
디자인 → 개발 → PM이라는 커리어 전환을 경험하며 다양한 시각에서 제품을 바라보고 있습니다.
이번 발표를 통해 PM을 꿈꾸거나 직무 전환을 고민하는 분들께 현실적인 인사이트와 작은 용기를 전할 수 있기를 바랍니다.`,
    image: "/img/profile_jiwon.jpeg",
    color: "#e5e6b4"
  },
  {
    id: 6,
    title: "개발 유튜버 할래말래 애매하긴해",
    content: "개발 유튜브 채널을 운영하며 겪은 수익, 콘텐츠 성과, 성장 전략 등을 공유하고, 잘되는 채널과 그렇지 않은 채널의 차이를 분석합니다. 유튜버를 꿈꾸는 분들을 위해 현실적인 조언과 방향성도 함께 전합니다.",
    speakerName: "김찬희",
    speakerIntro: `안녕하세요, 5년차 프론트엔드 개발자 김찬희입니다. 현재 주니어 프론트엔드 개발자를 대상으로 프론트맨이라는 채널을 운영하고 있으며, N잡과 오픈소스 프로젝트에 관심이 많습니다.`,
    image: "/img/profile_chanhee.jpg",
    color: "#d4fc79"
  },
  {
    id: 7,
    title: "풀스택 프리랜서가 AI시대에 프로젝트를 구성하는 방식",
    content: "AI 시대에 풀스택 프리랜서로서 어떻게 도구들을 조합해 프로젝트를 효율적으로 구성해왔는지에 대한 실질적인 경험과 시행착오를 공유합니다. ChatGPT, Cursor, Tailwind, Shadcn, Monorepo 등 각 도구의 도입 배경과 문제 해결 과정을 통해, 개발자의 역할이 어떻게 변화하고 있는지를 짚어봅니다.",
    speakerName: "최승일",
    speakerIntro: `중소 게임회사, 커머스 스타트업, 핀테크 스타트업을 거쳐 홀로서기에 도전중인 풀스택 개발자 최승일입니다.
생존을 위해 생산성에 관심이 많고, 생산성 관점에서 AI 제품군을 어떻게 대하고 있는지 이야기하고자 합니다.`,
    image: "/img/profile_seungil.png",
    color: "#fbc2eb"
  },
]

const openModal = (card: Card) => {
  selectedCard.value = card
  isModalOpen.value = true
  document.body.style.overflow = 'hidden'
}

const closeModal = () => {
  selectedCard.value = null
  isModalOpen.value = false
  document.body.style.overflow = 'auto'
}

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          // Add animation class for CSS-based animations
          if (cardElements.value.length > 0) {
            cardElements.value.forEach((card, index) => {
              if (card) {
                setTimeout(() => {
                  card.classList.add('animate-in')
                }, index * 100)
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
  } else {
    console.error('CardsRef not found')
  }
})
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
      >
        <div class="card-image">
          <img :src="card.image" :alt="card.title" loading="lazy" />
          <div class="card-overlay"></div>
        </div>
        
        <div class="card-content">
          <h3 class="card-title">{{ card.title }}</h3>
          <p class="card-text">{{ card.content }}</p>
          <button class="card-button" @click="openModal(card)">
            Learn More
            <span class="arrow">→</span>
          </button>
        </div>
        
        <div class="card-glow"></div>
      </div>
    </div>
    
    <!-- Modal Overlay -->
    <Transition name="modal">
      <div v-if="isModalOpen" class="modal-overlay" @click="closeModal">
        <div class="modal-content" :style="{ '--card-color': selectedCard?.color }" @click.stop>
          <button class="modal-close" @click="closeModal">
            <span>×</span>
          </button>
          
          <div class="modal-card">
            <div class="modal-image">
              <img :src="selectedCard?.image" :alt="selectedCard?.speakerName" loading="lazy" />
              <div class="modal-overlay-gradient"></div>
            </div>
            
            <div class="modal-info">
              <h3 class="modal-speaker-name">{{ selectedCard?.speakerName }}</h3>
              <h4 class="modal-title">{{ selectedCard?.title }}</h4>
              <p class="modal-intro">{{ selectedCard?.speakerIntro }}</p>
              
              <div class="modal-actions">
                <a 
                  v-if="selectedCard?.linkedinUrl" 
                  :href="selectedCard.linkedinUrl" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  class="linkedin-button"
                >
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                  </svg>
                  LinkedIn 프로필
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </Transition>
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
  color: #ffffff;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea, #764ba2, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.cards-header p {
  font-size: 1.2rem;
  color: #b8c5d1;
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
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  box-shadow: 
    0 10px 30px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              box-shadow 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              background-color 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              border-color 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  transform-style: preserve-3d;
  will-change: transform;
  transform: translateZ(0); /* Force GPU acceleration */
  
  /* Initial state for entrance animation */
  opacity: 0;
  transform: translate3d(0, 50px, 0) scale3d(0.9, 0.9, 1);
}

/* Entrance animation */
.floating-card.animate-in {
  opacity: 1;
  transform: translate3d(0, 0, 0) scale3d(1, 1, 1);
}

/* Hover animations - only transform and properties that don't cause reflow */
.floating-card:hover {
  background: rgba(255, 255, 255, 0.08);
  border-color: rgba(255, 255, 255, 0.15);
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.4),
    inset 0 1px 0 rgba(255, 255, 255, 0.15);
  transform: translate3d(0, -8px, 0) scale3d(1.02, 1.02, 1);
}

/* Active/click animation */
.floating-card:active {
  transform: translate3d(0, -4px, 0) scale3d(0.98, 0.98, 1);
  transition: transform 0.1s ease;
}

.card-image {
  position: relative;
  height: 300px;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  will-change: transform;
  transform: translateZ(0); /* Force GPU acceleration */
}

.floating-card:hover .card-image img {
  transform: translate3d(0, 0, 0) scale3d(1.05, 1.05, 1);
}

.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, var(--card-color, #667eea), transparent);
  opacity: 0.3;
  transition: opacity 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
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
  color: #ffffff;
  margin-bottom: 1rem;
}

.card-text {
  color: #b8c5d1;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.card-button {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #ffffff;
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              box-shadow 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              background-color 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94),
              border-color 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  display: flex;
  align-items: center;
  gap: 0.5rem;
  will-change: transform;
  transform: translateZ(0); /* Force GPU acceleration */
}

.card-button:hover {
  background: rgba(255, 255, 255, 0.12);
  border-color: rgba(255, 255, 255, 0.3);
  transform: translate3d(0, -2px, 0);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}

.card-button:active {
  transform: translate3d(0, 0, 0);
  transition: transform 0.1s ease;
}

.arrow {
  transition: transform 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  will-change: transform;
  transform: translateZ(0); /* Force GPU acceleration */
}

.card-button:hover .arrow {
  transform: translate3d(5px, 0, 0);
}

.card-glow {
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, var(--card-color, #667eea) 0%, transparent 70%);
  opacity: 0;
  transition: opacity 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  pointer-events: none;
  z-index: -1;
  will-change: opacity;
  transform: translateZ(0); /* Force GPU acceleration */
}

.floating-card:hover .card-glow {
  opacity: 0.1;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 2rem;
}

.modal-content {
  position: relative;
  max-width: 600px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(30px);
  -webkit-backdrop-filter: blur(30px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 24px;
  box-shadow: 
    0 20px 50px rgba(0, 0, 0, 0.5),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  transform: translateZ(0);
  animation: modalFlip 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

@keyframes modalFlip {
  0% {
    transform: perspective(1000px) rotateY(-90deg) scale(0.8);
    opacity: 0;
  }
  50% {
    transform: perspective(1000px) rotateY(-45deg) scale(0.9);
    opacity: 0.5;
  }
  100% {
    transform: perspective(1000px) rotateY(0deg) scale(1);
    opacity: 1;
  }
}

.modal-close {
  position: absolute;
  top: 1rem;
  right: 1rem;
  width: 40px;
  height: 40px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  color: #ffffff;
  font-size: 1.5rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  will-change: transform;
  transform: translateZ(0);
}

.modal-close:hover {
  background: rgba(255, 255, 255, 0.15);
  border-color: rgba(255, 255, 255, 0.3);
  transform: translate3d(0, 0, 0) scale(1.1);
}

.modal-card {
  position: relative;
  overflow: hidden;
}

.modal-image {
  position: relative;
  height: 350px;
  overflow: hidden;
  border-radius: 20px 20px 0 0;
}

.modal-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal-overlay-gradient {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  background: linear-gradient(
    to bottom,
    transparent 0%,
    rgba(0, 0, 0, 0.3) 50%,
    var(--card-color, #667eea) 100%
  );
  opacity: 0.8;
}

.modal-info {
  padding: 2rem;
}

.modal-speaker-name {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 0.5rem;
  background: linear-gradient(135deg, #667eea, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.modal-title {
  font-size: 1.3rem;
  font-weight: 600;
  color: #b8c5d1;
  margin-bottom: 1.5rem;
  line-height: 1.4;
}

.modal-intro {
  color: #e2e8f0;
  line-height: 1.7;
  font-size: 1rem;
  margin-bottom: 2rem;
  white-space: pre-line;
}

.modal-actions {
  display: flex;
  gap: 1rem;
}

.linkedin-button {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #ffffff;
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.95rem;
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  will-change: transform;
  transform: translateZ(0);
}

.linkedin-button:hover {
  background: rgba(255, 255, 255, 0.12);
  border-color: rgba(255, 255, 255, 0.3);
  transform: translate3d(0, -2px, 0);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  color: #ffffff;
}

.linkedin-button svg {
  flex-shrink: 0;
}

/* Modal Transition */
.modal-enter-active,
.modal-leave-active {
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(0.9);
}

.modal-enter-from .modal-content,
.modal-leave-to .modal-content {
  transform: perspective(1000px) rotateY(-90deg) scale(0.8);
}

@media (max-width: 1279px) {
  .floating-cards {
    padding: 1.5rem;
  }
  
  .cards-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .cards-header {
    margin-bottom: 3rem;
  }
  
  .cards-header h2 {
    font-size: 2.5rem;
    margin-bottom: 0.875rem;
  }
  
  .cards-header p {
    font-size: 1rem;
    max-width: 500px;
  }
  
  .floating-card {
    border-radius: 16px;
  }
  
  .card-content {
    padding: 1.5rem;
  }
  
  .card-title {
    font-size: 1.3rem;
    margin-bottom: 0.875rem;
  }
  
  .card-text {
    font-size: 0.95rem;
    line-height: 1.5;
    margin-bottom: 1.25rem;
  }
  
  .card-image {
    height: 300px;
  }
  
  .card-button {
    padding: 0.625rem 1.25rem;
    font-size: 0.95rem;
    border-radius: 40px;
  }
  
  /* Modal responsive styles */
  .modal-overlay {
    padding: 1rem;
  }
  
  .modal-content {
    max-height: 85vh;
    border-radius: 20px;
  }
  
  .modal-image {
    height: 350px;
    border-radius: 16px 16px 0 0;
  }
  
  .modal-info {
    padding: 1.5rem;
  }
  
  .modal-speaker-name {
    font-size: 1.5rem;
    margin-bottom: 0.375rem;
  }
  
  .modal-title {
    font-size: 1.1rem;
    margin-bottom: 1.25rem;
  }
  
  .modal-intro {
    font-size: 0.95rem;
    line-height: 1.6;
    margin-bottom: 1.5rem;
  }
  
  .linkedin-button {
    padding: 0.625rem 1.25rem;
    font-size: 0.9rem;
  }
}
</style>
