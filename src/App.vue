<template>
  <div class="app" @mousemove="handleMouseMove">
    <!-- Animated Background -->
    <div class="bg-canvas">
      <div class="bg-orb orb-1" :style="orbStyle(0.02)"></div>
      <div class="bg-orb orb-2" :style="orbStyle(-0.015)"></div>
      <div class="bg-orb orb-3" :style="orbStyle(0.01)"></div>
      <div class="bg-grid"></div>
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

.bg-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  opacity: 0.4;
  transition: transform 0.3s ease-out;
  will-change: transform;
}

.orb-1 {
  width: 500px;
  height: 500px;
  background: var(--accent-cyan);
  top: -150px;
  left: -100px;
  opacity: 0.15;
}

.orb-2 {
  width: 400px;
  height: 400px;
  background: var(--accent-purple);
  bottom: 10%;
  right: -80px;
  opacity: 0.12;
}

.orb-3 {
  width: 300px;
  height: 300px;
  background: var(--accent-blue);
  top: 50%;
  left: 40%;
  opacity: 0.08;
}

.bg-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.02) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%);
  -webkit-mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%);
}
</style>
