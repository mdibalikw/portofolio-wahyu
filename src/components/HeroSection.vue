<template>
  <section id="about" class="hero">
    <div class="container hero-container">
      <!-- Left Content -->
      <div class="hero-content" ref="contentRef">
        <div class="hero-badge" :class="{ visible: isVisible }">
          <span class="badge-dot"></span>
          <span>Available for Opportunities</span>
        </div>

        <h1 class="hero-name" :class="{ visible: isVisible }">
          <span class="line">
            <span class="word">Muhammad</span>
          </span>
          <span class="line">
            <span class="word gradient-text">Wahyu</span>
          </span>
        </h1>

        <div class="hero-role" :class="{ visible: isVisible }">
          <div class="role-line"></div>
          <span class="role-text">IT Professional</span>
        </div>

        <p class="hero-description" :class="{ visible: isVisible }">
          Berbasis di Jakarta, saya adalah seorang IT Professional dengan keahlian mendalam 
          dalam administrasi sistem, manajemen basis data, dan pengembangan aplikasi full-stack. 
          Saya memiliki ketertarikan besar dalam merancang solusi otomatisasi alur kerja, 
          integrasi sistem, dan implementasi arsitektur perangkat lunak skala perusahaan 
          untuk meningkatkan efisiensi operasional.
        </p>

        <div class="hero-actions" :class="{ visible: isVisible }">
          <button class="btn-primary" @click="$emit('navigate', 'projects')">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <rect x="3" y="3" width="7" height="7"/>
              <rect x="14" y="3" width="7" height="7"/>
              <rect x="14" y="14" width="7" height="7"/>
              <rect x="3" y="14" width="7" height="7"/>
            </svg>
            Lihat Proyek
          </button>
          <button class="btn-outline" @click="$emit('navigate', 'contact')">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
              <polyline points="22,6 12,13 2,6"/>
            </svg>
            Hubungi Saya
          </button>
        </div>

        <!-- Stats -->
        <div class="hero-stats" :class="{ visible: isVisible }">
          <div class="stat">
            <span class="stat-number">5+</span>
            <span class="stat-label">Teknologi</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-number">4+</span>
            <span class="stat-label">Proyek</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-number">∞</span>
            <span class="stat-label">Semangat</span>
          </div>
        </div>
      </div>

      <!-- Right Visual -->
      <div class="hero-visual" :class="{ visible: isVisible }">
        <div class="visual-wrapper">
          <!-- Floating Tech Icons -->
          <div class="floating-icon icon-1">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"/>
            </svg>
          </div>
          <div class="floating-icon icon-2">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <circle cx="12" cy="12" r="3"/><path d="M12 1v6m0 6v6m-7.071-3.071l4.243-4.243m4.243-4.243l4.243-4.243m-16.97 4.243l4.243 4.243m4.243 4.243l4.243 4.243"/>
            </svg>
          </div>
          <div class="floating-icon icon-3">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <ellipse cx="12" cy="5" rx="9" ry="3"/><path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"/><path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"/>
            </svg>
          </div>
          <div class="floating-icon icon-4">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
            </svg>
          </div>

          <!-- Central Glow -->
          <div class="central-element">
            <div class="glow-ring ring-1"></div>
            <div class="glow-ring ring-2"></div>
            <div class="glow-ring ring-3"></div>
            <div class="center-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/>
              </svg>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div class="scroll-indicator" :class="{ visible: isVisible }">
      <div class="mouse">
        <div class="wheel"></div>
      </div>
      <span>Scroll ke bawah</span>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

defineEmits(['navigate'])

const isVisible = ref(false)

onMounted(() => {
  setTimeout(() => {
    isVisible.value = true
  }, 200)
})
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  padding-top: var(--nav-height);
}

.hero-container {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 4rem;
  align-items: center;
  padding-top: 2rem;
  padding-bottom: 4rem;
}

/* Badge */
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0.5rem 1.2rem;
  background: rgba(6, 214, 160, 0.08);
  border: 1px solid rgba(6, 214, 160, 0.2);
  border-radius: 50px;
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--accent-cyan);
  margin-bottom: 2rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s var(--ease-out-expo) 0.1s;
}

.hero-badge.visible {
  opacity: 1;
  transform: translateY(0);
}

.badge-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--accent-cyan);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.5; transform: scale(1.3); }
}

/* Name */
.hero-name {
  font-size: clamp(3rem, 5.5vw, 4.5rem);
  font-weight: 800;
  line-height: 1.05;
  margin-bottom: 1.5rem;
  letter-spacing: -2px;
}

.hero-name .line {
  display: block;
  overflow: hidden;
}

.hero-name .word {
  display: inline-block;
  opacity: 0;
  transform: translateY(100%);
  transition: all 0.8s var(--ease-out-expo);
}

.hero-name.visible .line:nth-child(1) .word {
  opacity: 1;
  transform: translateY(0);
  transition-delay: 0.2s;
}

.hero-name.visible .line:nth-child(2) .word {
  opacity: 1;
  transform: translateY(0);
  transition-delay: 0.35s;
}

.gradient-text {
  background: var(--gradient-hero);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Role */
.hero-role {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
  opacity: 0;
  transform: translateX(-20px);
  transition: all 0.8s var(--ease-out-expo) 0.5s;
}

.hero-role.visible {
  opacity: 1;
  transform: translateX(0);
}

.role-line {
  width: 40px;
  height: 2px;
  background: var(--gradient-primary);
  border-radius: 1px;
}

.role-text {
  font-family: var(--font-mono);
  font-size: 1rem;
  color: var(--accent-cyan);
  letter-spacing: 2px;
  text-transform: uppercase;
}

/* Description */
.hero-description {
  color: var(--text-secondary);
  font-size: 1.05rem;
  line-height: 1.8;
  max-width: 520px;
  margin-bottom: 2.5rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s var(--ease-out-expo) 0.6s;
}

.hero-description.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Actions */
.hero-actions {
  display: flex;
  gap: 1rem;
  margin-bottom: 3rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s var(--ease-out-expo) 0.7s;
}

.hero-actions.visible {
  opacity: 1;
  transform: translateY(0);
}

.btn-primary,
.btn-outline {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0.85rem 1.8rem;
  border-radius: 12px;
  font-size: 0.95rem;
  font-weight: 600;
  transition: all 0.3s var(--ease-out-expo);
}

.btn-primary {
  background: var(--gradient-primary);
  color: var(--bg-primary);
  box-shadow: 0 4px 20px rgba(6, 214, 160, 0.25);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(6, 214, 160, 0.35);
}

.btn-outline {
  background: transparent;
  border: 1px solid var(--glass-border-hover);
  color: var(--text-primary);
}

.btn-outline:hover {
  background: rgba(255, 255, 255, 0.05);
  border-color: var(--accent-cyan);
  color: var(--accent-cyan);
  transform: translateY(-2px);
}

/* Stats */
.hero-stats {
  display: flex;
  align-items: center;
  gap: 2rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.8s var(--ease-out-expo) 0.85s;
}

.hero-stats.visible {
  opacity: 1;
  transform: translateY(0);
}

.stat {
  display: flex;
  flex-direction: column;
}

.stat-number {
  font-family: var(--font-heading);
  font-size: 1.8rem;
  font-weight: 700;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.stat-label {
  font-size: 0.8rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.stat-divider {
  width: 1px;
  height: 40px;
  background: var(--glass-border);
}

/* Visual Side */
.hero-visual {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  transform: scale(0.8);
  transition: all 1s var(--ease-out-expo) 0.4s;
}

.hero-visual.visible {
  opacity: 1;
  transform: scale(1);
}

.visual-wrapper {
  position: relative;
  width: 400px;
  height: 400px;
}

/* Floating Icons */
.floating-icon {
  position: absolute;
  width: 48px;
  height: 48px;
  padding: 12px;
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  border-radius: 14px;
  color: var(--accent-cyan);
  backdrop-filter: blur(10px);
  z-index: 2;
}

.icon-1 {
  top: 20px;
  left: 30px;
  animation: float 6s ease-in-out infinite;
}

.icon-2 {
  top: 10px;
  right: 40px;
  color: var(--accent-purple);
  animation: float 6s ease-in-out infinite 1s;
}

.icon-3 {
  bottom: 50px;
  left: 10px;
  color: var(--accent-blue);
  animation: float 6s ease-in-out infinite 2s;
}

.icon-4 {
  bottom: 30px;
  right: 20px;
  color: var(--accent-pink);
  animation: float 6s ease-in-out infinite 3s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-15px); }
}

/* Central Element */
.central-element {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 200px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.glow-ring {
  position: absolute;
  border-radius: 50%;
  border: 1px solid;
}

.ring-1 {
  width: 200px;
  height: 200px;
  border-color: rgba(6, 214, 160, 0.15);
  animation: ring-spin 20s linear infinite;
}

.ring-2 {
  width: 150px;
  height: 150px;
  border-color: rgba(14, 165, 233, 0.15);
  animation: ring-spin 15s linear infinite reverse;
}

.ring-3 {
  width: 100px;
  height: 100px;
  border-color: rgba(139, 92, 246, 0.2);
  animation: ring-spin 10s linear infinite;
}

@keyframes ring-spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.center-icon {
  width: 60px;
  height: 60px;
  padding: 14px;
  background: var(--gradient-primary);
  border-radius: 18px;
  color: var(--bg-primary);
  box-shadow: 0 0 40px rgba(6, 214, 160, 0.3);
  z-index: 2;
}

/* Scroll Indicator */
.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.8rem;
  opacity: 0;
  transition: all 0.8s var(--ease-out-expo) 1.2s;
}

.scroll-indicator.visible {
  opacity: 1;
}

.mouse {
  width: 24px;
  height: 38px;
  border: 2px solid var(--glass-border-hover);
  border-radius: 12px;
  display: flex;
  justify-content: center;
  padding-top: 6px;
}

.wheel {
  width: 4px;
  height: 8px;
  background: var(--accent-cyan);
  border-radius: 2px;
  animation: scroll-wheel 2s ease-in-out infinite;
}

@keyframes scroll-wheel {
  0% { opacity: 1; transform: translateY(0); }
  100% { opacity: 0; transform: translateY(12px); }
}

.scroll-indicator span {
  font-size: 0.7rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 2px;
}

/* Responsive */
@media (max-width: 992px) {
  .hero-container {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 3rem;
  }

  .hero-description {
    margin: 0 auto 2.5rem;
  }

  .hero-actions {
    justify-content: center;
  }

  .hero-stats {
    justify-content: center;
  }

  .hero-badge {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-role {
    justify-content: center;
  }

  .visual-wrapper {
    width: 300px;
    height: 300px;
  }
}

@media (max-width: 576px) {
  .hero-name {
    font-size: 2.5rem;
    letter-spacing: -1px;
  }

  .hero-actions {
    flex-direction: column;
  }

  .hero-stats {
    gap: 1.5rem;
  }

  .visual-wrapper {
    width: 250px;
    height: 250px;
  }
}
</style>
