<template>
  <section id="projects" class="projects-section">
    <div class="container">
      <div class="section-header" ref="headerRef">
        <span class="section-tag" :class="{ visible: headerVisible }">
          <span class="tag-icon">◆</span> Portofolio
        </span>
        <h2 class="section-title" :class="{ visible: headerVisible }">
           <span class="gradient-text">Proyek</span>
        </h2>
        <p class="section-subtitle" :class="{ visible: headerVisible }">
          Beberapa proyek yang mencerminkan pengalaman dan kemampuan teknis saya
        </p>
      </div>

      <div class="projects-grid" @mousemove="handleMouseMove">
        <div
          v-for="(project, index) in projects"
          :key="project.title"
          class="project-card"
          :class="{ visible: cardVisible[index] }"
          :ref="el => setCardRef(el, index)"
        >
          <!-- Spotlight Border & Background (Dynamic 2.0) -->
          <div class="spotlight-border"></div>
          <div class="spotlight-bg"></div>

          <!-- Card Accent Line -->
          <div class="card-accent" :style="{ background: project.accent }"></div>

          <div class="card-body">
            <!-- Header -->
            <div class="card-header">
              <div class="project-number">{{ String(index + 1).padStart(2, '0') }}</div>
              <div class="project-icon" :style="{ color: project.iconColor }">
                <!-- Dashboard Icon -->
                <svg v-if="project.icon === 'dashboard'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
                  <line x1="9" y1="17" x2="9" y2="10"/>
                  <line x1="15" y1="17" x2="15" y2="12"/>
                  <line x1="12" y1="17" x2="12" y2="7"/>
                </svg>
                <!-- Folder Icon -->
                <svg v-else-if="project.icon === 'folder'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/>
                  <line x1="12" y1="11" x2="12" y2="17"/>
                  <line x1="9" y1="14" x2="15" y2="14"/>
                </svg>
                <!-- File/Document Icon -->
                <svg v-else-if="project.icon === 'file'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
                  <polyline points="14 2 14 8 20 8"/>
                  <line x1="16" y1="13" x2="8" y2="13"/>
                  <line x1="16" y1="17" x2="8" y2="17"/>
                </svg>
                <!-- Book Icon -->
                <svg v-else-if="project.icon === 'book'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/>
                  <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/>
                </svg>
                <!-- Chat Icon -->
                <svg v-else-if="project.icon === 'chat'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/>
                </svg>
                <!-- Default Code Icon -->
                <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="28" height="28">
                  <polyline points="16 18 22 12 16 6"/>
                  <polyline points="8 6 2 12 8 18"/>
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
    title: 'Dashboard Pelaporan Real-Time M-Files (MFWS)',
    description: 'Mesin dashboard pelaporan berbasis konfigurasi real-time yang terhubung langsung ke REST API M-Files Web Service (MFWS). Menampilkan visualisasi data vault menggunakan grafik interaktif modern, dengan penelusuran metadata rekursif paralel (Promise-based), caching in-memory, dan pencegahan token storm.',
    tags: ['Node.js', 'Vue 3', 'Tailwind CSS', 'M-Files API', 'Express'],
    accent: 'linear-gradient(180deg, #06d6a0, transparent)',
    iconColor: '#06d6a0',
    tagBorder: 'rgba(6, 214, 160, 0.25)',
    tagColor: '#06d6a0',
    dots: ['#06d6a0', '#0ea5e9', '#8b5cf6', '#f59e0b'],
    icon: 'dashboard'
  },
  {
    title: 'Taxonomy Auto-Provisioning Admin Panel',
    description: 'Mini-aplikasi berbasis Node.js (Express) dan Vanilla JS (UI) untuk melakukan auto-provisioning (pembuatan taksonomi/folder massal) ke OpenText Content Server melalui REST API. Dilengkapi manajemen autentikasi in-memory browser yang aman.',
    tags: ['Node.js', 'Express', 'Vanilla JS', 'OpenText API', 'Glassmorphism'],
    accent: 'linear-gradient(180deg, #0ea5e9, transparent)',
    iconColor: '#0ea5e9',
    tagBorder: 'rgba(14, 165, 233, 0.25)',
    tagColor: '#0ea5e9',
    dots: ['#0ea5e9', '#8b5cf6', '#06d6a0', '#ef4444'],
    icon: 'folder'
  },
  {
    title: 'Pengembangan Sistem ECM & Manajemen HR',
    description: 'Merancang dan mengonfigurasi sistem manajemen SDM multi-kelas menggunakan M-Files, serta mengatur Retention Schedule Information dan sistem Manajemen Arsip (Records Management) di OpenText Content Server.',
    tags: ['M-Files', 'OpenText OTCS', 'Records Mgmt'],
    accent: 'linear-gradient(180deg, #8b5cf6, transparent)',
    iconColor: '#8b5cf6',
    tagBorder: 'rgba(139, 92, 246, 0.25)',
    tagColor: '#8b5cf6',
    dots: ['#8b5cf6', '#0ea5e9', '#06d6a0'],
    icon: 'file'
  },
  {
    title: 'Aplikasi Virtual Chat AI Kustom',
    description: 'Mengembangkan aplikasi virtual chat mandiri yang diintegrasikan dengan model AI terkuantisasi (format .gguf) dan dataset kustom untuk kebutuhan interaksi spesifik.',
    tags: ['Python', 'AI (.gguf)', 'NLP'],
    accent: 'linear-gradient(180deg, #ec4899, transparent)',
    iconColor: '#ec4899',
    tagBorder: 'rgba(236, 72, 153, 0.25)',
    tagColor: '#ec4899',
    dots: ['#ec4899', '#8b5cf6', '#06d6a0'],
    icon: 'chat'
  },
  {
    title: 'Aplikasi Web Manajemen Buku (Full-Stack)',
    description: 'Membangun sistem manajemen buku end-to-end yang mencakup perancangan API (CRUD), konfigurasi CORS, dan implementasi antarmuka pengguna yang responsif.',
    tags: ['Laravel', 'Vue.js', 'REST API'],
    accent: 'linear-gradient(180deg, #f59e0b, transparent)',
    iconColor: '#f59e0b',
    tagBorder: 'rgba(245, 158, 11, 0.25)',
    tagColor: '#f59e0b',
    dots: ['#f59e0b', '#06d6a0', '#0ea5e9'],
    icon: 'book'
  }
]

const headerRef = ref(null)
const headerVisible = ref(false)
const cardVisible = ref(projects.map(() => false))
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
  background: rgba(255, 255, 255, 0.015);
  border-radius: 24px;
  overflow: hidden;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.7s var(--ease-out-expo), transform 0.3s ease;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
}

.project-card::before {
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

.project-card.visible {
  opacity: 1;
  transform: translateY(0);
}

.project-card:hover {
  transform: translateY(-4px);
}

/* Spotlight Dynamic 2.0 */
.spotlight-border {
  position: absolute;
  inset: 0;
  border-radius: inherit;
  padding: 1px;
  background: radial-gradient(
    600px circle at var(--mouse-x, 0) var(--mouse-y, 0),
    rgba(255, 255, 255, 0.3),
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
    600px circle at var(--mouse-x, 0) var(--mouse-y, 0),
    rgba(255, 255, 255, 0.03),
    transparent 40%
  );
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  z-index: 0;
}

.projects-grid:hover .spotlight-border,
.projects-grid:hover .spotlight-bg {
  opacity: 1;
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
