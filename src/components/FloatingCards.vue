<script setup lang="ts">
import { onMounted, ref } from 'vue'

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
    title: "Redis Lettuce 기반 분산 락으로 데이터 정합성 보장하기",
    content: "Redis Lettuce 기반 분산 락을 통해 주문·결제 등에서 발생할 수 있는 중복 처리 문제를 해결하고, 동시성 환경에서도 데이터 정합성을 보장하는 구조와 실제 적용 사례를 소개합니다. 또한 락 해제의 한계와 향후 개선 방향까지 함께 다룹니다.",
    image: "https://s.abcnews.com/images/Business/GTY_steve_jobs_2_jtm_150323.jpg",
    color: "#667eea"
  },
  {
    id: 2,
    title: "현업에서의 LLMOps",
    content: "현업에서의 경험을 바탕으로 LLMOps 워크플로우 전반—데이터 준비, 모델 운영, 모니터링 등—에서 실제로 어떤 작업이 이루어지는지 설명합니다. 또한 다양한 LLMOps 도구들을 소개하며 실무에 적용할 수 있는 방안들을 함께 제시합니다.",
    image: "https://hips.hearstapps.com/hmg-prod/images/elon-musk-gettyimages-2147789844-web-675b2c17301ea.jpg",
    color: "#764ba2"
  },
  {
    id: 3,
    title: "지구 반대편을 대응하는 어플리케이션을 위해",
    content: "글로벌 서비스를 운영하며 겪은 다국어, 현지 정책, UI 분기 등의 어려움을 주니어 개발자의 시각으로 풀어낸 경험을 공유합니다. 지구 반대편 사용자도 자연스럽게 사용할 수 있는 서비스를 만들기 위해 고민한 실질적인 방법들을 소개합니다.",
    image: "https://ca.slack-edge.com/T053C7SL8GL-U08P06Q702X-1287f6bb6f7d-512",
    color: "#f093fb"
  },
  {
    id: 4,
    title: "알잘딱 에이전트 만들기: Context Engineering",
    content: "행위 중심의 에이전트를 효과적으로 만들기 위해선 LLM의 한계를 극복할 수 있는 정교한 Context Engineering이 핵심이며, 이를 위해 LangChain/LangGraph 같은 도구들이 활용됩니다. 또한 에이전트의 품질을 평가할 수 있는 지표 없이 실서비스에 안정적으로 적용하기 어렵다는 점도 강조합니다.",
    image: "https://media.licdn.com/dms/image/v2/D5603AQE92humOXxvaQ/profile-displayphoto-shrink_800_800/B56ZW.KqRIGUAg-/0/1742652223402?e=1757548800&v=beta&t=UII61jRmTGddJ1pzsHexDVi1tfb2DEe2hQ5tjHb5OW4",
    color: "#f5576c"
  },
  {
    id: 5,
    title: "디자이너 출신 개발자의 PM 도전기",
    content: "디자인 전공 후 프론트엔드 개발자로 일하다가 PM 인턴으로 커리어를 확장하게 된 개인적인 여정과 동기를 공유합니다. 개발자에서 PM으로 전환하기까지의 준비 과정과 실제 경험을 솔직하게 들려드립니다.",
    image: "https://lh3.google.com/u/0/d/1GtwKsWAM5BoIm1DmoVh9ckrGhGT64Sm5=k",
    color: "#e5e6b4"
  },
  {
    id: 6,
    title: "개발 유튜버 할래말래 애매하긴해",
    content: "개발 유튜브 채널을 운영하며 겪은 수익, 콘텐츠 성과, 성장 전략 등을 공유하고, 잘되는 채널과 그렇지 않은 채널의 차이를 분석합니다. 유튜버를 꿈꾸는 분들을 위해 현실적인 조언과 방향성도 함께 전합니다.",
    image: "https://pimg.mk.co.kr/news/cms/202502/04/news-p.v1.20250204.c58974823543481ba7070079cffe568b_R.jpg",
    color: "#d4fc79"
  },
  {
    id: 7,
    title: "풀스택 프리랜서가 AI시대에 프로젝트를 구성하는 방식",
    content: "AI 시대에 풀스택 프리랜서로서 어떻게 도구들을 조합해 프로젝트를 효율적으로 구성해왔는지에 대한 실질적인 경험과 시행착오를 공유합니다. ChatGPT, Cursor, Tailwind, Shadcn, Monorepo 등 각 도구의 도입 배경과 문제 해결 과정을 통해, 개발자의 역할이 어떻게 변화하고 있는지를 짚어봅니다.",
    image: "https://i.namu.wiki/i/C9DriGKF1EAL2ScL7E7ojp9ReOUt0PVWrhTdUQgIr2lYcxSIa9qR8ydH0lVysRvTKNTLnqA9jZ5MiLBYnVxuRw.webp",
    color: "#fbc2eb"
  },
]

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
}
</style>
