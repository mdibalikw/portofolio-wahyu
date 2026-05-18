<template>
  <section id="skills" class="skills-section">
    <div class="container">
      <div class="section-header" ref="headerRef">
        <span class="section-tag" :class="{ visible: headerVisible }">
          <span class="tag-icon">◆</span> Kompetensi Inti
        </span>
        <h2 class="section-title" :class="{ visible: headerVisible }">
          Keahlian <span class="gradient-text">Saya</span>
        </h2>
        <p class="section-subtitle" :class="{ visible: headerVisible }">
          Teknologi dan platform yang saya kuasai untuk membangun solusi enterprise yang handal
        </p>
      </div>

      <div class="skills-grid" @mousemove="handleMouseMove">
        <div
          v-for="(skill, index) in skills"
          :key="skill.title"
          class="skill-card"
          :class="{ visible: cardVisible[index] }"
          :ref="el => setCardRef(el, index)"
        >
          <!-- Spotlight Border & Background (Dynamic 2.0) -->
          <div class="spotlight-border"></div>
          <div class="spotlight-bg"></div>

          <div class="card-glow" :style="{ background: skill.glowColor }"></div>
          <div class="card-content">
            <div class="card-icon" :style="{ color: skill.iconColor }">
              <component :is="skill.icon" />
            </div>
            <h3 class="card-title">{{ skill.title }}</h3>
            <div class="card-tags">
              <span v-for="tag in skill.tags" :key="tag" class="tech-tag">{{ tag }}</span>
            </div>
            <div class="progress-container">
              <div class="progress-header">
                <span class="progress-label">Proficiency</span>
                <span class="progress-value" :class="{ visible: cardVisible[index] }">{{ skill.level }}%</span>
              </div>
              <div class="progress-track">
                <div
                  class="progress-fill"
                  :style="{
                    width: cardVisible[index] ? skill.level + '%' : '0%',
                    background: skill.gradient
                  }"
                ></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, h, markRaw } from 'vue'

// SVG Icon Components
const CodeIcon = markRaw({
  render() {
    return h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round', width: '32', height: '32' }, [
      h('polyline', { points: '16 18 22 12 16 6' }),
      h('polyline', { points: '8 6 2 12 8 18' }),
      h('line', { x1: '12', y1: '2', x2: '12', y2: '22', 'stroke-dasharray': '2 4' })
    ])
  }
})

const ServerIcon = markRaw({
  render() {
    return h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round', width: '32', height: '32' }, [
      h('rect', { x: '2', y: '2', width: '20', height: '8', rx: '2', ry: '2' }),
      h('rect', { x: '2', y: '14', width: '20', height: '8', rx: '2', ry: '2' }),
      h('line', { x1: '6', y1: '6', x2: '6.01', y2: '6' }),
      h('line', { x1: '6', y1: '18', x2: '6.01', y2: '18' })
    ])
  }
})

const GearIcon = markRaw({
  render() {
    return h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round', width: '32', height: '32' }, [
      h('circle', { cx: '12', cy: '12', r: '3' }),
      h('path', { d: 'M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z' })
    ])
  }
})

const DatabaseIcon = markRaw({
  render() {
    return h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round', width: '32', height: '32' }, [
      h('ellipse', { cx: '12', cy: '5', rx: '9', ry: '3' }),
      h('path', { d: 'M21 12c0 1.66-4 3-9 3s-9-1.34-9-3' }),
      h('path', { d: 'M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5' })
    ])
  }
})

const ChipIcon = markRaw({
  render() {
    return h('svg', { viewBox: '0 0 24 24', fill: 'none', stroke: 'currentColor', 'stroke-width': '1.5', 'stroke-linecap': 'round', 'stroke-linejoin': 'round', width: '32', height: '32' }, [
      h('rect', { x: '4', y: '4', width: '16', height: '16', rx: '2' }),
      h('rect', { x: '9', y: '9', width: '6', height: '6' }),
      h('line', { x1: '9', y1: '1', x2: '9', y2: '4' }),
      h('line', { x1: '15', y1: '1', x2: '15', y2: '4' }),
      h('line', { x1: '9', y1: '20', x2: '9', y2: '23' }),
      h('line', { x1: '15', y1: '20', x2: '15', y2: '23' }),
      h('line', { x1: '20', y1: '9', x2: '23', y2: '9' }),
      h('line', { x1: '20', y1: '14', x2: '23', y2: '14' }),
      h('line', { x1: '1', y1: '9', x2: '4', y2: '9' }),
      h('line', { x1: '1', y1: '14', x2: '4', y2: '14' })
    ])
  }
})

const skills = [
  {
    title: 'Pengembangan Web',
    tags: ['Laravel', 'Vue.js', 'WordPress', 'Elementor'],
    level: 90,
    icon: CodeIcon,
    iconColor: '#06d6a0',
    glowColor: 'rgba(6, 214, 160, 0.06)',
    gradient: 'linear-gradient(90deg, #06d6a0, #0ea5e9)'
  },
  {
    title: 'Sistem Enterprise & ECM',
    tags: ['OpenText OTCS', 'AppWorks', 'M-Files'],
    level: 85,
    icon: ServerIcon,
    iconColor: '#0ea5e9',
    glowColor: 'rgba(14, 165, 233, 0.06)',
    gradient: 'linear-gradient(90deg, #0ea5e9, #8b5cf6)'
  },
  {
    title: 'Otomatisasi & Integrasi',
    tags: ['n8n', 'IDP', 'OCR'],
    level: 80,
    icon: GearIcon,
    iconColor: '#8b5cf6',
    glowColor: 'rgba(139, 92, 246, 0.06)',
    gradient: 'linear-gradient(90deg, #8b5cf6, #ec4899)'
  },
  {
    title: 'Basis Data & Infrastruktur',
    tags: ['SQL Server', 'Database Admin', 'DevOps'],
    level: 85,
    icon: DatabaseIcon,
    iconColor: '#f59e0b',
    glowColor: 'rgba(245, 158, 11, 0.06)',
    gradient: 'linear-gradient(90deg, #f59e0b, #ef4444)'
  },
  {
    title: 'AI & Python',
    tags: ['Python', 'Model .gguf', 'AI Integration'],
    level: 75,
    icon: ChipIcon,
    iconColor: '#ec4899',
    glowColor: 'rgba(236, 72, 153, 0.06)',
    gradient: 'linear-gradient(90deg, #ec4899, #06d6a0)'
  }
]

const headerRef = ref(null)
const headerVisible = ref(false)
const cardVisible = ref(skills.map(() => false))
const cardRefs = ref([])

function handleMouseMove(e) {
  for (const card of cardRefs.value) {
    if (!card) continue;
    const rect = card.getBoundingClientRect();
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
    card.style.setProperty('--mouse-x', `${x}px`);
    card.style.setProperty('--mouse-y', `${y}px`);
  }
}

function setCardRef(el, index) {
  if (el) cardRefs.value[index] = el
}

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          if (entry.target === headerRef.value) {
            headerVisible.value = true
          }
          const cardIndex = cardRefs.value.indexOf(entry.target)
          if (cardIndex !== -1) {
            setTimeout(() => {
              cardVisible.value[cardIndex] = true
            }, cardIndex * 120)
          }
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.15 }
  )

  if (headerRef.value) observer.observe(headerRef.value)
  cardRefs.value.forEach(el => {
    if (el) observer.observe(el)
  })

  onUnmounted(() => observer.disconnect())
})
</script>

<style scoped>
.skills-section {
  padding: 8rem 0;
  position: relative;
}

/* Section Header */
.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-tag {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--accent-cyan);
  text-transform: uppercase;
  letter-spacing: 3px;
  margin-bottom: 1rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s var(--ease-out-expo);
}

.section-tag.visible {
  opacity: 1;
  transform: translateY(0);
}

.tag-icon {
  font-size: 0.6rem;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 700;
  margin-bottom: 1rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s var(--ease-out-expo) 0.1s;
}

.section-title.visible {
  opacity: 1;
  transform: translateY(0);
}

.gradient-text {
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-subtitle {
  color: var(--text-secondary);
  font-size: 1.05rem;
  max-width: 500px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s var(--ease-out-expo) 0.2s;
}

.section-subtitle.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Skills Grid */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 1.5rem;
}

/* Skill Card */
.skill-card {
  position: relative;
  background: rgba(255, 255, 255, 0.015);
  border-radius: 24px;
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s var(--ease-out-expo), transform 0.3s ease;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
}

.skill-card::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1px;
  background: rgba(255, 255, 255, 0.04);
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
}

.skill-card.visible {
  opacity: 1;
  transform: translateY(0);
}

.skill-card:hover {
  transform: translateY(-4px);
}

/* Spotlight Dynamic 2.0 */
.spotlight-border {
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1px;
  background: radial-gradient(
    500px circle at var(--mouse-x, 0) var(--mouse-y, 0),
    rgba(255, 255, 255, 0.25),
    transparent 40%
  );
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  z-index: 2;
}

.spotlight-bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(
    500px circle at var(--mouse-x, 0) var(--mouse-y, 0),
    rgba(255, 255, 255, 0.03),
    transparent 40%
  );
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  z-index: 0;
}

.skills-grid:hover .spotlight-border,
.skills-grid:hover .spotlight-bg {
  opacity: 1;
}

.card-glow {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 0.4s ease;
}

.skill-card:hover .card-glow {
  opacity: 1;
}

.card-content {
  position: relative;
  z-index: 1;
  padding: 2rem;
}

.card-icon {
  margin-bottom: 1.5rem;
  transition: transform 0.3s var(--ease-spring);
}

.skill-card:hover .card-icon {
  transform: scale(1.1);
}

.card-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.card-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tech-tag {
  font-size: 0.75rem;
  font-family: var(--font-mono);
  padding: 0.3rem 0.75rem;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 6px;
  color: var(--text-secondary);
  transition: all 0.3s ease;
}

.skill-card:hover .tech-tag {
  border-color: rgba(255, 255, 255, 0.1);
  background: rgba(255, 255, 255, 0.06);
}

/* Progress Bar */
.progress-container {
  margin-top: auto;
}

.progress-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.progress-label {
  font-size: 0.75rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.progress-value {
  font-size: 0.8rem;
  font-family: var(--font-mono);
  font-weight: 500;
  color: var(--text-secondary);
  opacity: 0;
  transition: opacity 0.5s ease 0.5s;
}

.progress-value.visible {
  opacity: 1;
}

.progress-track {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.06);
  border-radius: 3px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  border-radius: 3px;
  width: 0%;
  transition: width 1.5s cubic-bezier(0.1, 0.5, 0.1, 1) 0.3s;
  box-shadow: 0 0 10px rgba(6, 214, 160, 0.3);
}

/* Responsive */
@media (max-width: 768px) {
  .skills-section {
    padding: 5rem 0;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>
