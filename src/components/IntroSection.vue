<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const introRef = ref<HTMLElement>()
const titleRef = ref<HTMLElement>()
const contentRef = ref<HTMLElement>()

onMounted(() => {
  console.log('IntroSection mounted')
  
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        console.log('Intersection observed:', entry.isIntersecting, entry.intersectionRatio)
        
        if (entry.isIntersecting) {
          console.log('Starting intro animations')
          
          // Animate title
          if (titleRef.value) {
            gsap.fromTo(titleRef.value,
              { opacity: 0, y: 50 },
              { 
                opacity: 1, 
                y: 0, 
                duration: 1, 
                ease: "power2.out",
                onComplete: () => console.log('Title animation complete')
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
                onComplete: () => console.log('Content animation complete')
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
    console.log('Observer attached to intro section')
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
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor 
            incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud 
            exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
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
            <button class="cta-button">
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
  color: #333;
  margin-bottom: 2rem;
  line-height: 1.2;
  background: linear-gradient(135deg, #667eea, #764ba2);
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
  color: #666;
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
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  border: none;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  font-weight: 600;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.6);
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
  opacity: 0.1;
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
