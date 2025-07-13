<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const titleRef = ref<HTMLElement>()
const subtitleRef = ref<HTMLElement>()

onMounted(() => {
  setTimeout(() => {
    // Subtitle animation with delay
    if (subtitleRef.value) {
      gsap.fromTo(subtitleRef.value,
        {
          opacity: 0,
          y: 30
        },
        {
          opacity: 1,
          y: 0,
          duration: 1.5,
          delay: 0.5,
          ease: "power2.out"
        }
      )
    }
  }, 100)
})
</script>

<template>
  <div ref="heroRef" class="sipe-hero">
    <div class="hero-content">
      <h1 ref="titleRef" class="hero-title">
        <span>SIPE</span>
        <span>4TH</span>
        <span>CONFERENCE</span>
      </h1>
      <h2 ref="subtitleRef" class="hero-subtitle">
        네 번째 사담콘
      </h2>
    </div>
    <div class="floating-elements">
      <div class="float-circle float-1"></div>
      <div class="float-circle float-2"></div>
      <div class="float-circle float-3"></div>
      <div class="float-triangle float-4"></div>
      <div class="float-triangle float-5"></div>
    </div>
  </div>
</template>

<style scoped>
.sipe-hero {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  background: radial-gradient(ellipse at center, 
    rgba(26, 26, 46, 0.9) 0%, 
    rgba(15, 15, 35, 0.95) 50%, 
    rgba(10, 10, 15, 1) 100%
  );
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.hero-content {
  z-index: 10;
  max-width: 1280px;
  padding: 2rem;
}

.hero-title {
  font-weight: 900;
  font-size: clamp(4rem, 10vw, 9rem);
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #667eea, #764ba2, #a8edea);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: none;
  line-height: 1.1;
  font-family: 'Inter', sans-serif;
  opacity: 1;
  display: flex;
  flex-direction: column;
  gap: 0.1em;
}

.hero-subtitle {
  font-size: clamp(2rem, 3vw, 3rem);
  font-weight: 300;
  color: rgba(255, 255, 255, 0.9);
  letter-spacing: 0.05em;
  opacity: 1;
  transform: translateY(0);
  margin-top: 2rem;
}

.floating-elements {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 1;
}

.float-circle {
  position: absolute;
  border-radius: 50%;
  background: rgba(102, 126, 234, 0.15);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.float-triangle {
  position: absolute;
  width: 0;
  height: 0;
  filter: blur(1px);
}

.float-1 {
  width: 120px;
  height: 120px;
  top: 10%;
  left: 10%;
  animation: float1 6s ease-in-out infinite;
}

.float-2 {
  width: 80px;
  height: 80px;
  top: 20%;
  right: 15%;
  animation: float2 8s ease-in-out infinite;
}

.float-3 {
  width: 150px;
  height: 150px;
  bottom: 20%;
  left: 15%;
  animation: float3 7s ease-in-out infinite;
}

.float-4 {
  border-left: 30px solid transparent;
  border-right: 30px solid transparent;
  border-bottom: 50px solid rgba(102, 126, 234, 0.15);
  top: 60%;
  right: 20%;
  animation: float4 5s ease-in-out infinite;
}

.float-5 {
  border-left: 25px solid transparent;
  border-right: 25px solid transparent;
  border-bottom: 40px solid rgba(118, 75, 162, 0.12);
  bottom: 30%;
  right: 10%;
  animation: float5 9s ease-in-out infinite;
}

@keyframes float1 {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-30px) rotate(180deg); }
}

@keyframes float2 {
  0%, 100% { transform: translateY(0px) scale(1); }
  50% { transform: translateY(-40px) scale(1.2); }
}

@keyframes float3 {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(-180deg); }
}

@keyframes float4 {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-25px) rotate(120deg); }
}

@keyframes float5 {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-35px) rotate(-120deg); }
}

/* Responsive design */
@media (max-width: 1279px) {
  .sipe-hero {
    padding: 1rem;
  }
  
  .hero-content {
    padding: 0;
    max-width: 100%;
  }
  
  .hero-title {
    font-size: clamp(2rem, 11vw, 6rem);
    margin-bottom: 1.5rem;
    gap: 0.08em;
  }

  .hero-subtitle {
    font-size: clamp(1.5rem, 4vw, 2.5rem);
    margin-top: 1.5rem;
    font-weight: 400;
  }
  
  .floating-elements {
    opacity: 0.7;
  }
  
  .float-circle {
    opacity: 0.4;
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
  }
  
  .float-triangle {
    opacity: 0.3;
    filter: blur(0.5px);
  }
  
  .float-1 {
    width: 80px;
    height: 80px;
    top: 15%;
    left: 8%;
  }
  
  .float-2 {
    width: 60px;
    height: 60px;
    top: 25%;
    right: 12%;
  }
  
  .float-3 {
    width: 100px;
    height: 100px;
    bottom: 25%;
    left: 12%;
  }
  
  .float-4 {
    border-left: 20px solid transparent;
    border-right: 20px solid transparent;
    border-bottom: 35px solid rgba(102, 126, 234, 0.12);
    top: 55%;
    right: 15%;
  }
  
  .float-5 {
    border-left: 18px solid transparent;
    border-right: 18px solid transparent;
    border-bottom: 30px solid rgba(118, 75, 162, 0.1);
    bottom: 35%;
    right: 8%;
  }
}
</style>
