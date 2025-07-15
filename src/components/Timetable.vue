<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const timetableRef = ref<HTMLElement>()
const timetableContentRef = ref<HTMLElement>()

interface Session {
  time: string
  duration: string
  title: string
  speaker?: string
  type?: 'keynote' | 'session' | 'break' | 'closing'
}

const sessions: Session[] = [
  {
    time: '13:00 ~ 13:30',
    duration: '30분',
    title: '등록 및 입장',
    type: 'break'
  },
  {
    time: '13:30 ~ 13:40',
    duration: '10분',
    title: 'KEYNOTE: SIPE 소개 및 행사 안내',
    speaker: '심미진',
    type: 'keynote'
  },
  {
    time: '13:40 ~ 14:10',
    duration: '30분',
    title: 'Redis Lettuce 기반 분산 락으로 데이터 정합성 보장하기',
    speaker: '장준환',
    type: 'session'
  },
  {
    time: '14:10 ~ 14:30',
    duration: '20분',
    title: 'Real-World LLMOps',
    speaker: '김민준',
    type: 'session'
  },
  {
    time: '14:30 ~ 14:50',
    duration: '20분',
    title: '쉬는 시간',
    type: 'break'
  },
  {
    time: '14:50 ~ 15:10',
    duration: '20분',
    title: '지구 반대편을 대응하는 어플리케이션을 위해',
    speaker: '김민규',
    type: 'session'
  },
  {
    time: '15:10 ~ 15:40',
    duration: '30분',
    title: '알잘딱 AI 에이전트 만들기 w. 컨텍스트 엔지니어링',
    speaker: '조혜정',
    type: 'session'
  },
  {
    time: '15:40 ~ 16:00',
    duration: '20분',
    title: '쉬는 시간',
    type: 'break'
  },
  {
    time: '16:00 ~ 16:20',
    duration: '20분',
    title: '디자이너 출신 개발자의 PM 도전기',
    speaker: '이지원',
    type: 'session'
  },
  {
    time: '16:20 ~ 16:40',
    duration: '20분',
    title: '개발 유튜버 할래말래 애매하긴해',
    speaker: '김찬희',
    type: 'session'
  },
  {
    time: '16:40 ~ 17:00',
    duration: '20분',
    title: '풀스택 프리랜서가 AI시대에 프로젝트를 구성하는 방식',
    speaker: '최승일',
    type: 'session'
  },
  {
    time: '17:00 ~ 17:30',
    duration: '30분',
    title: '행사 마무리 (이벤트, 사진 촬영 및 정리)',
    type: 'closing'
  }
]

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          if (timetableContentRef.value) {
            gsap.fromTo(timetableContentRef.value,
              { opacity: 0, y: 50 },
              { 
                opacity: 1, 
                y: 0, 
                duration: 1, 
                ease: "power2.out",
              }
            )
            
            // Animate session items with stagger
            const sessionItems = timetableContentRef.value.querySelectorAll('.session-item')
            gsap.fromTo(sessionItems,
              { opacity: 0, y: 30 },
              { 
                opacity: 1, 
                y: 0, 
                duration: 0.6, 
                ease: "power2.out",
                stagger: 0.1,
                delay: 0.3
              }
            )
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

  if (timetableRef.value) {
    observer.observe(timetableRef.value)
  }
})

const getSessionTypeClass = (type?: string) => {
  switch (type) {
    case 'keynote':
      return 'session-keynote'
    case 'break':
      return 'session-break'
    case 'closing':
      return 'session-closing'
    default:
      return 'session-default'
  }
}
</script>

<template>
  <div ref="timetableRef" class="timetable-section">
    <div class="timetable-container">
      <div class="timetable-header">
        <h2>프로그램 안내</h2>
        <p>SIPE 네 번째 사담콘의 상세 프로그램을 확인해보세요</p>
      </div>
      
      <div ref="timetableContentRef" class="timetable-content">
        <div class="timetable-card">
          <div class="sessions-list">
            <div
              v-for="(session, index) in sessions"
              :key="index"
              class="session-item"
              :class="getSessionTypeClass(session.type)"
            >
              <div class="session-time">
                <div class="time-display">{{ session.time }}</div>
                <div class="duration-display">{{ session.duration }}</div>
              </div>
              
              <div class="session-content">
                <h3 class="session-title">{{ session.title }}</h3>
                
                <div v-if="session.speaker">
                  <span class="speaker-name">{{ session.speaker }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.timetable-section {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 4rem 2rem;
}

.timetable-container {
  width: 100%;
}

.timetable-header {
  text-align: center;
  margin-bottom: 4rem;
}

.timetable-header h2 {
  font-size: 3rem;
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea, #764ba2, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.timetable-header p {
  font-size: 1.2rem;
  color: #b8c5d1;
  max-width: 600px;
  margin: 0 auto;
}

.timetable-content {
  opacity: 0;
}

.timetable-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 24px;
  padding: 3rem;
  box-shadow: 
    0 20px 50px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
  transition: transform 0.3s ease;
  will-change: transform;
  transform: translate3d(0, 0, 0);
}

.timetable-card:hover {
  transform: translate3d(0, -8px, 0);
}

.sessions-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.session-item {
  display: flex;
  gap: 2rem;
  padding: 2rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  transition: all 0.3s ease;
  will-change: transform, opacity;
  transform: translate3d(0, 0, 0);
  position: relative;
  overflow: hidden;
}

.session-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(255, 255, 255, 0.02);
  border-radius: 16px;
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
}

.session-item:hover {
  transform: translate3d(0, -4px, 0);
  border-color: rgba(255, 255, 255, 0.15);
}

.session-item:hover::before {
  opacity: 1;
}

/* Session type specific styling */
.session-keynote {
  border-left: 4px solid #667eea;
  background: rgba(102, 126, 234, 0.05);
}

.session-break {
  border-left: 4px solid #a8edea;
  background: rgba(168, 237, 234, 0.05);
}

.session-closing {
  border-left: 4px solid #764ba2;
  background: rgba(118, 75, 162, 0.05);
}

.session-default {
  border-left: 4px solid #f093fb;
  background: rgba(240, 147, 251, 0.05);
}

.session-time {
  flex-shrink: 0;
  min-width: 140px;
  text-align: center;
}

.time-display {
  font-size: 1.1rem;
  font-weight: 600;
  color: #ffffff;
  margin-bottom: 0.5rem;
}

.duration-display {
  font-size: 0.9rem;
  color: #a8edea;
  background: rgba(168, 237, 234, 0.1);
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  display: inline-block;
}

.session-content {
  flex: 1;
}

.session-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #ffffff;
  margin-bottom: 0.75rem;
  line-height: 1.4;
}

.speaker-name {
  font-size: 1rem;
  font-weight: 500;
  color: #667eea;
  background: rgba(102, 126, 234, 0.1);
  padding: 0.375rem 0.875rem;
  border-radius: 20px;
  display: inline-block;
}

@media (max-width: 1279px) {
  .timetable-section {
    min-height: auto;
    padding: 3rem 1.5rem;
  }
  
  .timetable-header {
    margin-bottom: 3rem;
  }
  
  .timetable-header h2 {
    font-size: 2.5rem;
    margin-bottom: 0.875rem;
  }
  
  .timetable-header p {
    font-size: 1rem;
    max-width: 500px;
  }
  
  .timetable-card {
    padding: 2rem;
    border-radius: 20px;
  }
  
  .session-time {
    min-width: auto;
    text-align: left;
  }
  
  .time-display {
    font-size: 1rem;
    margin-bottom: 0.375rem;
  }
  
  .duration-display {
    font-size: 0.8rem;
    padding: 0.2rem 0.6rem;
  }
  
  .session-title {
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
  }
}

@media (max-width: 767px) {
  .timetable-section {
    padding: 2rem 1rem;
  }
  
  .timetable-header {
    margin-bottom: 2rem;
  }
  
  .timetable-header h2 {
    font-size: 2rem;
  }
  
  .timetable-header p {
    font-size: 0.9rem;
  }
  
  .timetable-card {
    padding: 1.5rem;
  }
  
  .sessions-list {
    gap: 1rem;
  }
  
  .session-item {
    flex-direction: column;
    padding: 1.25rem;
    gap: 0.75rem;
    border-radius: 12px;
  }

  .session-item::before {
    border-radius: 12px;
  }
  
  .session-title {
    font-size: 1.1rem;
    line-height: 1.3;
  }
}
</style>
