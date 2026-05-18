<template>
  <nav class="navbar" :class="{ scrolled: isScrolled, 'menu-open': isMobileMenuOpen }">
    <div class="nav-container">
      <a href="#" class="logo" @click.prevent="$emit('navigate', 'hero')">
        <span class="logo-text">MW</span>
        <span class="logo-dot">.</span>
      </a>

      <ul class="nav-links" :class="{ open: isMobileMenuOpen }">
        <li v-for="link in links" :key="link.id">
          <a
            :href="'#' + link.id"
            :class="{ active: activeSection === link.id }"
            @click.prevent="handleNav(link.id)"
          >
            <span class="nav-indicator"></span>
            {{ link.label }}
          </a>
        </li>
      </ul>

      <button
        class="hamburger"
        :class="{ active: isMobileMenuOpen }"
        @click="isMobileMenuOpen = !isMobileMenuOpen"
        aria-label="Toggle menu"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

defineProps({
  activeSection: { type: String, default: 'hero' }
})

const emit = defineEmits(['navigate'])

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)

const links = [
  { id: 'about', label: 'Tentang' },
  { id: 'skills', label: 'Keahlian' },
  { id: 'projects', label: 'Proyek' },
  { id: 'contact', label: 'Kontak' }
]

function handleNav(id) {
  emit('navigate', id)
  isMobileMenuOpen.value = false
}

function checkScroll() {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', checkScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', checkScroll)
})
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  padding: 0;
  transition: all 0.4s var(--ease-out-expo);
}

.navbar::before {
  content: '';
  position: absolute;
  inset: 0;
  background: rgba(6, 10, 19, 0);
  backdrop-filter: blur(0px);
  -webkit-backdrop-filter: blur(0px);
  border-bottom: 1px solid transparent;
  transition: all 0.4s var(--ease-out-expo);
}

.navbar.scrolled::before {
  background: rgba(6, 10, 19, 0.8);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--glass-border);
}

.nav-container {
  position: relative;
  z-index: 1;
  max-width: var(--container-max);
  margin: 0 auto;
  padding: 1.2rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: padding 0.4s var(--ease-out-expo);
}

.navbar.scrolled .nav-container {
  padding: 0.8rem 2rem;
}

/* Logo */
.logo {
  display: flex;
  align-items: center;
  gap: 0;
  font-family: var(--font-heading);
  font-size: 1.8rem;
  font-weight: 800;
  letter-spacing: -1px;
}

.logo-text {
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.logo-dot {
  color: var(--accent-cyan);
  font-size: 2.2rem;
  line-height: 1;
}

/* Navigation Links */
.nav-links {
  display: flex;
  gap: 0.5rem;
}

.nav-links a {
  position: relative;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.6rem 1.2rem;
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-secondary);
  border-radius: 10px;
  transition: all 0.3s ease;
}

.nav-links a:hover {
  color: var(--text-primary);
  background: rgba(255, 255, 255, 0.04);
}

.nav-links a.active {
  color: var(--accent-cyan);
}

.nav-indicator {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--accent-cyan);
  opacity: 0;
  transform: scale(0);
  transition: all 0.3s var(--ease-spring);
}

.nav-links a.active .nav-indicator {
  opacity: 1;
  transform: scale(1);
}

/* Hamburger */
.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  padding: 8px;
  z-index: 10;
}

.hamburger span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--text-primary);
  border-radius: 2px;
  transition: all 0.3s ease;
  transform-origin: center;
}

.hamburger.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
  transform: scaleX(0);
}

.hamburger.active span:nth-child(3) {
  transform: rotate(-45deg) translate(5px, -5px);
}

/* Mobile */
@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }

  .nav-links {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    background: rgba(6, 10, 19, 0.95);
    backdrop-filter: blur(30px);
    -webkit-backdrop-filter: blur(30px);
    opacity: 0;
    visibility: hidden;
    transition: all 0.4s var(--ease-out-expo);
  }

  .nav-links.open {
    opacity: 1;
    visibility: visible;
  }

  .nav-links a {
    font-size: 1.2rem;
    padding: 1rem 2rem;
  }
}
</style>
