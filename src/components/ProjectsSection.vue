<template>
  <section id="projects" class="projects-section">
    <div class="container">
      <div class="section-header" ref="headerRef">
        <span class="section-tag" :class="{ visible: headerVisible }">
          <span class="tag-icon">◆</span> Portofolio
        </span>
        <h2 class="section-title" :class="{ visible: headerVisible }">
          Proyek <span class="gradient-text">Unggulan</span>
        </h2>
        <p class="section-subtitle" :class="{ visible: headerVisible }">
          Beberapa proyek yang mencerminkan pengalaman dan kemampuan teknis saya
        </p>
      </div>

      <div class="projects-grid">
        <div
          v-for="(project, index) in projects"
          :key="project.title"
          class="project-card"
          :class="{ visible: cardVisible[index] }"
          :ref="el => setCardRef(el, index)"
          @mouseenter="activeCard = index"
          @mouseleave="activeCard = null"
        >
          <!-- Card Accent Line -->
          <div class="card-accent" :style="{ background: project.accent }"></div>

          <div class="card-body">
            <!-- Header -->
            <div class="card-header">
              <div class="project-number">{{ String(index + 1).padStart(2, '0') }}</div>
              <div class="project-icon" :style="{ color: project.iconColor }">
                <svg v-if="index === 0" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
                  <polyline points="14 2 14 8 20 8"/>
                  <line x1="16" y1="13" x2="8" y2="13"/>
                  <line x1="16" y1="17" x2="8" y2="17"/>
                </svg>
                <svg v-else-if="index === 1" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/>
                  <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/>
                </svg>
                <svg v-else-if="index === 2" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <polyline points="16 18 22 12 16 6"/>
                  <polyline points="8 6 2 12 8 18"/>
                </svg>
                <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
                </svg>
              </div>
            </div>

            <!-- Tags -->
            <div class="project-tags">
              <span
                v-for="tag in project.tags"
                :key="tag"
                class="tag"
                :style="{ borderColor: project.tagBorder, color: project.tagColor }"
              >
                {{ tag }}
              </span>
            </div>

            <!-- Content -->
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-desc">{{ project.description }}</p>

            <!-- Footer -->
            <div class="card-footer">
              <div class="tech-stack">
                <span class="stack-label">Tech Stack</span>
                <div class="stack-dots">
                  <span
                    v-for="(dot, i) in project.dots"
                    :key="i"
                    class="dot"
                    :style="{ background: dot }"
                    :title="project.tags[i] || ''"
                  ></span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const projects = [
  {
    title: 'Pengembangan Sistem ECM & Manajemen HR',
    description: 'Merancang dan mengonfigurasi sistem manajemen SDM multi-kelas menggunakan M-Files, serta mengatur Retention Schedule Information dan sistem Manajemen Arsip (Records Management) di OpenText Content Server.',
    tags: ['M-Files', 'OpenText OTCS', 'Records Mgmt'],
    accent: 'linear-gradient(180deg, #06d6a0, transparent)',
    iconColor: '#06d6a0',
    tagBorder: 'rgba(6, 214, 160, 0.25)',
    tagColor: '#06d6a0',
    dots: ['#06d6a0', '#0ea5e9', '#8b5cf6']
  },
  {
    title: 'Aplikasi Web Manajemen Buku (Full-Stack)',
    description: 'Membangun sistem manajemen buku end-to-end yang mencakup perancangan API (CRUD), konfigurasi CORS, dan implementasi antarmuka pengguna yang responsif.',
    tags: ['Laravel', 'Vue.js', 'REST API'],
    accent: 'linear-gradient(180deg, #0ea5e9, transparent)',
    iconColor: '#0ea5e9',
    tagBorder: 'rgba(14, 165, 233, 0.25)',
    tagColor: '#0ea5e9',
    dots: ['#0ea5e9', '#06d6a0', '#f59e0b']
  },
  {
    title: 'Sistem Proses Aplikasi Kredit & Otomatisasi',
    description: 'Membangun proses aplikasi kredit dengan pemodelan BPMN dan merancang alur kerja otomatisasi persetujuan. Menggunakan n8n untuk integrasi Intelligent Document Processing (IDP) dan ekstraksi OCR.',
    tags: ['AppWorks', 'n8n', 'BPMN', 'IDP'],
    accent: 'linear-gradient(180deg, #8b5cf6, transparent)',
    iconColor: '#8b5cf6',
    tagBorder: 'rgba(139, 92, 246, 0.25)',
    tagColor: '#8b5cf6',
    dots: ['#8b5cf6', '#ec4899', '#0ea5e9', '#06d6a0']
  },
  {
    title: 'Aplikasi Virtual Chat AI Kustom',
    description: 'Mengembangkan aplikasi virtual chat mandiri yang diintegrasikan dengan model AI terkuantisasi (format .gguf) dan dataset kustom untuk kebutuhan interaksi spesifik.',
    tags: ['Python', 'AI (.gguf)', 'NLP'],
    accent: 'linear-gradient(180deg, #ec4899, transparent)',
    iconColor: '#ec4899',
    tagBorder: 'rgba(236, 72, 153, 0.25)',
    tagColor: '#ec4899',
    dots: ['#ec4899', '#8b5cf6', '#06d6a0']
  }
]

const headerRef = ref(null)
const headerVisible = ref(false)
const cardVisible = ref(projects.map(() => false))
const cardRefs = ref([])
const activeCard = ref(null)

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
            }, cardIndex * 150)
          }
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.1 }
  )

  if (headerRef.value) observer.observe(headerRef.value)
  cardRefs.value.forEach(el => {
    if (el) observer.observe(el)
  })

  onUnmounted(() => observer.disconnect())
})
</script>

<style scoped>
.projects-section {
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
  background: var(--gradient-secondary);
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

/* Projects Grid */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
}

/* Project Card */
.project-card {
  position: relative;
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  border-radius: 20px;
  overflow: hidden;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.7s var(--ease-out-expo),
              border-color 0.3s ease,
              box-shadow 0.3s ease;
}

.project-card.visible {
  opacity: 1;
  transform: translateY(0);
}

.project-card:hover {
  border-color: var(--glass-border-hover);
  transform: translateY(-6px);
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.4);
}

.card-accent {
  position: absolute;
  top: 0;
  left: 0;
  width: 3px;
  height: 100%;
  opacity: 0.6;
  transition: opacity 0.3s ease;
}

.project-card:hover .card-accent {
  opacity: 1;
}

.card-body {
  padding: 2.5rem;
  position: relative;
  z-index: 1;
}

/* Header */
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.project-number {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: var(--text-muted);
  letter-spacing: 1px;
}

.project-icon {
  transition: transform 0.3s var(--ease-spring);
}

.project-card:hover .project-icon {
  transform: scale(1.15) rotate(5deg);
}

/* Tags */
.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tag {
  font-size: 0.7rem;
  font-family: var(--font-mono);
  padding: 0.25rem 0.7rem;
  border: 1px solid;
  border-radius: 6px;
  background: rgba(255, 255, 255, 0.02);
  transition: all 0.3s ease;
}

.project-card:hover .tag {
  background: rgba(255, 255, 255, 0.04);
}

/* Content */
.project-title {
  font-size: 1.3rem;
  font-weight: 600;
  line-height: 1.3;
  margin-bottom: 1rem;
  transition: color 0.3s ease;
}

.project-desc {
  color: var(--text-secondary);
  font-size: 0.95rem;
  line-height: 1.7;
  margin-bottom: 2rem;
}

/* Footer */
.card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 1.5rem;
  border-top: 1px solid var(--glass-border);
}

.stack-label {
  font-size: 0.7rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 1px;
  display: block;
  margin-bottom: 0.5rem;
}

.stack-dots {
  display: flex;
  gap: 0.4rem;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  transition: transform 0.3s var(--ease-spring);
}

.project-card:hover .dot {
  transform: scale(1.3);
}

/* Responsive */
@media (max-width: 992px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 576px) {
  .card-body {
    padding: 1.5rem;
  }
}
</style>
