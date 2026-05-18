<template>
  <section id="contact" class="contact-section">
    <div class="container">
      <div class="contact-wrapper" ref="wrapperRef" :class="{ visible: isVisible }">
        <!-- Left Side -->
        <div class="contact-info">
          <span class="section-tag">
            <span class="tag-icon">◆</span> Kontak
          </span>
          <h2 class="contact-title">
            Mari <span class="gradient-text">Terhubung</span>
          </h2>
          <p class="contact-desc">
            Saya selalu terbuka untuk mendiskusikan peluang baru, kolaborasi proyek, 
            atau sekadar berbagi ide seputar teknologi.
          </p>

          <div class="info-items">
            <div class="info-item">
              <div class="info-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="22" height="22">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/>
                  <circle cx="12" cy="10" r="3"/>
                </svg>
              </div>
              <div>
                <span class="info-label">Lokasi</span>
                <span class="info-value">Jakarta, Indonesia</span>
              </div>
            </div>

            <a href="mailto:mwahyuii79@gmail.com" class="info-item clickable">
              <div class="info-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" width="22" height="22">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                  <polyline points="22,6 12,13 2,6"/>
                </svg>
              </div>
              <div>
                <span class="info-label">Email</span>
                <span class="info-value">mwahyuii79@gmail.com</span>
              </div>
            </a>
          </div>

          <!-- Social Links -->
          <div class="social-links">
            <a
              v-for="social in socials"
              :key="social.label"
              :href="social.url"
              target="_blank"
              rel="noopener noreferrer"
              class="social-btn"
              :aria-label="social.label"
            >
              <span class="social-icon" v-html="social.icon"></span>
              <span class="social-label">{{ social.label }}</span>
              <svg class="arrow-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="14" height="14">
                <line x1="7" y1="17" x2="17" y2="7"/>
                <polyline points="7 7 17 7 17 17"/>
              </svg>
            </a>
          </div>
        </div>

        <!-- Right Side - Decorative -->
        <div class="contact-visual">
          <div class="visual-card">
            <div class="terminal-header">
              <span class="terminal-dot" style="background: #ff5f56"></span>
              <span class="terminal-dot" style="background: #ffbd2e"></span>
              <span class="terminal-dot" style="background: #27c93f"></span>
              <span class="terminal-title">contact.js</span>
            </div>
            <div class="terminal-body">
              <div class="code-line">
                <span class="line-num">1</span>
                <span class="keyword">const</span> <span class="variable">developer</span> <span class="operator">=</span> <span class="bracket">{</span>
              </div>
              <div class="code-line">
                <span class="line-num">2</span>
                <span class="indent"></span><span class="property">name</span><span class="operator">:</span> <span class="string">"Muhammad Wahyu"</span><span class="comma">,</span>
              </div>
              <div class="code-line">
                <span class="line-num">3</span>
                <span class="indent"></span><span class="property">role</span><span class="operator">:</span> <span class="string">"IT Professional"</span><span class="comma">,</span>
              </div>
              <div class="code-line">
                <span class="line-num">4</span>
                <span class="indent"></span><span class="property">location</span><span class="operator">:</span> <span class="string">"Jakarta 🇮🇩"</span><span class="comma">,</span>
              </div>
              <div class="code-line">
                <span class="line-num">5</span>
                <span class="indent"></span><span class="property">available</span><span class="operator">:</span> <span class="boolean">true</span><span class="comma">,</span>
              </div>
              <div class="code-line">
                <span class="line-num">6</span>
                <span class="indent"></span><span class="property">skills</span><span class="operator">:</span> <span class="bracket">[</span><span class="string">"Vue"</span><span class="comma">,</span> <span class="string">"Laravel"</span><span class="comma">,</span> <span class="string">"..."</span><span class="bracket">]</span>
              </div>
              <div class="code-line">
                <span class="line-num">7</span>
                <span class="bracket">}</span><span class="operator">;</span>
              </div>
              <div class="code-line blink-line">
                <span class="line-num">8</span>
                <span class="cursor">|</span>
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

const wrapperRef = ref(null)
const isVisible = ref(false)

const socials = [
  {
    label: 'LinkedIn',
    url: 'https://www.linkedin.com/in/muhammad-wahyu-b4b73a1b3/',
    icon: '<svg viewBox="0 0 24 24" fill="currentColor" width="20" height="20"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/></svg>'
  },
  {
    label: 'GitHub',
    url: 'https://github.com/mdibalikw',
    icon: '<svg viewBox="0 0 24 24" fill="currentColor" width="20" height="20"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>'
  }
]

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isVisible.value = true
        observer.disconnect()
      }
    },
    { threshold: 0.15 }
  )

  if (wrapperRef.value) observer.observe(wrapperRef.value)

  onUnmounted(() => observer.disconnect())
})
</script>

<style scoped>
.contact-section {
  padding: 8rem 0;
  position: relative;
}

.contact-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  background: var(--glass-bg);
  border: 1px solid var(--glass-border);
  border-radius: 24px;
  padding: 4rem;
  opacity: 0;
  transform: translateY(40px);
  transition: all 0.8s var(--ease-out-expo);
}

.contact-wrapper.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Section Tag */
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
}

.tag-icon {
  font-size: 0.6rem;
}

/* Title */
.contact-title {
  font-size: clamp(2rem, 3.5vw, 2.5rem);
  font-weight: 700;
  margin-bottom: 1rem;
}

.gradient-text {
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.contact-desc {
  color: var(--text-secondary);
  font-size: 1rem;
  line-height: 1.7;
  margin-bottom: 2.5rem;
}

/* Info Items */
.info-items {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  margin-bottom: 2.5rem;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem 1.2rem;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid var(--glass-border);
  border-radius: 14px;
  transition: all 0.3s ease;
}

.info-item.clickable:hover {
  background: rgba(6, 214, 160, 0.05);
  border-color: rgba(6, 214, 160, 0.2);
  transform: translateX(4px);
}

.info-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  background: rgba(6, 214, 160, 0.08);
  border-radius: 12px;
  color: var(--accent-cyan);
  flex-shrink: 0;
}

.info-label {
  display: block;
  font-size: 0.75rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 0.15rem;
}

.info-value {
  font-size: 0.95rem;
  color: var(--text-primary);
  font-weight: 500;
}

/* Social Links */
.social-links {
  display: flex;
  gap: 1rem;
}

.social-btn {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0.75rem 1.4rem;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid var(--glass-border);
  border-radius: 12px;
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-primary);
  transition: all 0.3s var(--ease-out-expo);
}

.social-btn:hover {
  background: rgba(6, 214, 160, 0.08);
  border-color: rgba(6, 214, 160, 0.3);
  transform: translateY(-3px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
}

.social-icon {
  display: flex;
  color: var(--accent-cyan);
}

.social-label {
  font-weight: 500;
}

.arrow-icon {
  margin-left: auto;
  opacity: 0;
  transform: translate(-5px, 5px);
  transition: all 0.3s ease;
}

.social-btn:hover .arrow-icon {
  opacity: 0.5;
  transform: translate(0, 0);
}

/* Terminal / Code Card */
.contact-visual {
  display: flex;
  justify-content: center;
}

.visual-card {
  width: 100%;
  max-width: 420px;
  background: rgba(13, 19, 33, 0.8);
  border: 1px solid var(--glass-border);
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
}

.terminal-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem 1.2rem;
  background: rgba(255, 255, 255, 0.03);
  border-bottom: 1px solid var(--glass-border);
}

.terminal-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.terminal-title {
  margin-left: auto;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--text-muted);
}

.terminal-body {
  padding: 1.5rem;
  font-family: var(--font-mono);
  font-size: 0.85rem;
  line-height: 2;
}

.code-line {
  display: flex;
  align-items: center;
  white-space: nowrap;
}

.line-num {
  width: 30px;
  color: var(--text-muted);
  opacity: 0.4;
  font-size: 0.75rem;
  user-select: none;
  flex-shrink: 0;
}

.indent {
  width: 1.5rem;
  display: inline-block;
}

.keyword { color: #c792ea; }
.variable { color: #82aaff; }
.operator { color: var(--text-muted); margin: 0 0.25rem; }
.bracket { color: #ffcb6b; }
.property { color: #f07178; }
.string { color: #c3e88d; }
.boolean { color: #ff5370; }
.comma { color: var(--text-muted); }

.cursor {
  color: var(--accent-cyan);
  animation: blink 1.2s step-end infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

/* Responsive */
@media (max-width: 992px) {
  .contact-wrapper {
    grid-template-columns: 1fr;
    gap: 3rem;
    padding: 3rem 2rem;
  }
}

@media (max-width: 576px) {
  .contact-wrapper {
    padding: 2rem 1.5rem;
  }

  .social-links {
    flex-direction: column;
  }

  .visual-card {
    max-width: 100%;
  }
}
</style>
