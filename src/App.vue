<template>
  <div class="app" @mousemove="handleMouseMove">
    <!-- Animated Background Dark Dynamic 2.0 -->
    <div class="bg-canvas">
      <div class="bg-aurora" :style="orbStyle(0.015)"></div>
      <div class="bg-grid"></div>
      <div class="bg-noise"></div>
    </div>

    <NavBar :active-section="activeSection" @navigate="scrollToSection" />
    <HeroSection @navigate="scrollToSection" />
    <SkillsSection />
    <ProjectsSection />
    <ContactSection />
    <FooterSection />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'

const mouseX = ref(0)
const mouseY = ref(0)
const activeSection = ref('hero')

function handleMouseMove(e) {
  mouseX.value = e.clientX
  mouseY.value = e.clientY
}

function orbStyle(factor) {
  return {
    transform: `translate(${mouseX.value * factor}px, ${mouseY.value * factor}px)`
  }
}

function scrollToSection(sectionId) {
  const el = document.getElementById(sectionId)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' })
  }
}

function handleScroll() {
  const sections = ['contact', 'projects', 'skills', 'about']
  for (const id of sections) {
    const el = document.getElementById(id)
    if (el) {
      const rect = el.getBoundingClientRect()
      if (rect.top <= 200) {
        activeSection.value = id
        break
      }
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.app {
  position: relative;
  min-height: 100vh;
}

.bg-canvas {
  position: fixed;
  inset: 0;
  z-index: -1;
  overflow: hidden;
  pointer-events: none;
}

.bg-noise {
  position: absolute;
  inset: 0;
  z-index: 1;
  opacity: 0.04;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
  pointer-events: none;
}

.bg-aurora {
  position: absolute;
  top: -20%;
  left: -20%;
  width: 140%;
  height: 140%;
  background: 
    radial-gradient(800px circle at 20% 30%, rgba(6, 214, 160, 0.05) 0%, transparent 60%),
    radial-gradient(1000px circle at 80% 80%, rgba(139, 92, 246, 0.05) 0%, transparent 60%),
    radial-gradient(900px circle at 60% 20%, rgba(14, 165, 233, 0.05) 0%, transparent 60%);
  filter: blur(60px);
  animation: aurora-move 20s linear infinite alternate;
  will-change: transform;
}

@keyframes aurora-move {
  0% { transform: rotate(0deg) scale(1); }
  50% { transform: rotate(5deg) scale(1.05); }
  100% { transform: rotate(-5deg) scale(1); }
}

.bg-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.015) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.015) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse at center, black 40%, transparent 80%);
  -webkit-mask-image: radial-gradient(ellipse at center, black 40%, transparent 80%);
}
</style>
