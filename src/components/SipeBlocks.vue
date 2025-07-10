<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'

const titleRef = ref<HTMLElement>()
const subtitleRef = ref<HTMLElement>()

onMounted(() => {
  console.log('SipeBlocks mounted')
  
  // Wait a bit for DOM to be ready
  setTimeout(() => {
    console.log('Starting GSAP animations for title')
    
    // Initial animation for title
    if (titleRef.value) {
      gsap.fromTo(titleRef.value, 
        { 
          scale: 0.5, 
          opacity: 0,
          y: -50
        },
        { 
          scale: 1, 
          opacity: 1,
          y: 0,
          duration: 2,
          ease: "elastic.out(1, 0.3)",
          onComplete: () => console.log('Title animation complete')
        }
      )
    }

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

    // Continuous floating animation for title
    if (titleRef.value) {
      gsap.to(titleRef.value, {
        y: "random(-10, 10)",
        rotation: "random(-1, 1)",
        duration: "random(4, 6)",
        repeat: -1,
        yoyo: true,
        ease: "sine.inOut"
      })
    }
  }, 100)
})
</script>

<template>
  <div class="sipe-hero">
    <div class="hero-content">
      <h1 ref="titleRef" class="hero-title">
        <span class="title-line title-sipe">SIPE</span>
        <span class="title-line title-4th">4th</span>
        <span class="title-line title-conference">CONFERENCE</span>
      </h1>
      <p ref="subtitleRef" class="hero-subtitle">
        네 번째 사담콘
      </p>
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
  background: linear-gradient(135deg, 
    #74b9ff 0%,   /* Light blue */
    #0984e3 25%,  /* Blue */
    #00b894 50%,  /* Mint green */
    #00cec9 75%,  /* Cyan */
    #6c5ce7 100%  /* Purple blue */
  );
  background-size: 400% 400%;
  animation: gradientShift 8s ease-in-out infinite;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.hero-content {
  text-align: center;
  z-index: 10;
  max-width: 1280px;
  padding: 2rem;
}

.hero-title {
  font-weight: 900;
  letter-spacing: 0.1em;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #ff9595, #ffe5b1);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: none;
  line-height: 1.1;
  font-family: 'Inter', sans-serif;
  opacity: 1;
  transform: translateY(0) skewX(-8deg);
  font-style: italic;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.1em;
}

.title-line {
  display: block;
  white-space: nowrap;
  text-align: center;
  width: 100%;
}

/* Adjust font sizes to make lines appear equal width */
.title-sipe {
  font-size: clamp(3rem, 8vw, 7rem);
  letter-spacing: 0.3em;
}

.title-4th {
  font-size: clamp(4rem, 10vw, 9rem);
  letter-spacing: 0.4em;
}

.title-conference {
  font-size: clamp(2.2rem, 6vw, 5.5rem);
  letter-spacing: 0.15em;
}

.hero-subtitle {
  font-size: clamp(1.2rem, 3vw, 2rem);
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
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
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
  border-bottom: 50px solid rgba(255, 255, 255, 0.1);
  top: 60%;
  right: 20%;
  animation: float4 5s ease-in-out infinite;
}

.float-5 {
  border-left: 25px solid transparent;
  border-right: 25px solid transparent;
  border-bottom: 40px solid rgba(255, 255, 255, 0.08);
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
@media (max-width: 768px) {
  .hero-content {
    padding: 1rem;
  }
  
  .hero-title {
    transform: translateY(0) skewX(-6deg);
  }
  
  .title-sipe {
    font-size: clamp(2rem, 6vw, 4rem);
    letter-spacing: 0.2em;
  }

  .title-4th {
    font-size: clamp(2.5rem, 7vw, 5rem);
    letter-spacing: 0.3em;
  }

  .title-conference {
    font-size: clamp(1.5rem, 4.5vw, 3rem);
    letter-spacing: 0.1em;
  }
  
  .hero-subtitle {
    font-size: clamp(1rem, 2.5vw, 1.5rem);
  }
  
  .float-circle {
    opacity: 0.5;
  }
  
  .float-triangle {
    opacity: 0.3;
  }
  
  .float-1 {
    width: 80px;
    height: 80px;
  }
  
  .float-2 {
    width: 60px;
    height: 60px;
  }
  
  .float-3 {
    width: 100px;
    height: 100px;
  }
}

@media (max-width: 480px) {
  .hero-title {
    transform: translateY(0) skewX(-4deg);
    gap: 0.05em;
  }
  
  .title-sipe {
    font-size: clamp(1.5rem, 5vw, 2.5rem);
    letter-spacing: 0.15em;
  }

  .title-4th {
    font-size: clamp(2rem, 6vw, 3.2rem);
    letter-spacing: 0.25em;
  }

  .title-conference {
    font-size: clamp(1.2rem, 3.5vw, 2rem);
    letter-spacing: 0.08em;
  }
  
  .hero-subtitle {
    font-size: clamp(0.9rem, 2vw, 1.2rem);
  }
}
</style>
