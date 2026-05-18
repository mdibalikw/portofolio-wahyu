<template>
  <footer class="site-footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-brand">
          <span class="footer-logo">MW<span class="dot">.</span></span>
        </div>
        <p class="footer-text">
          &copy; {{ currentYear }} Muhammad Wahyu. Dibuat dengan
          <span class="heart">♥</span>
          menggunakan Vue.js
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.site-footer {
  padding: 2.5rem 0;
  border-top: 1px solid var(--glass-border);
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-logo {
  font-family: var(--font-heading);
  font-size: 1.3rem;
  font-weight: 800;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.dot {
  color: var(--accent-cyan);
}

.footer-text {
  font-size: 0.85rem;
  color: var(--text-muted);
}

.heart {
  color: var(--accent-pink);
  display: inline-block;
  animation: heartbeat 1.5s ease infinite;
}

@keyframes heartbeat {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.2); }
}

@media (max-width: 576px) {
  .footer-content {
    flex-direction: column;
    gap: 0.8rem;
    text-align: center;
  }
}
</style>
