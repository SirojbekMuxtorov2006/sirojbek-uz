<script setup>
import { inject } from 'vue'

const t = inject('t')
</script>

<template>
  <section class="hero-section">
    <!-- Animated background orbs -->
    <div class="blob blob-1"></div>
    <div class="blob blob-2"></div>
    <div class="blob blob-3"></div>
    <div class="dots-overlay"></div>

    <div class="container hero-container">
      <div class="hero-content">
        <div class="greeting-badge">
          <span class="pulse-dot"></span>
          <span>{{ t('hero.badge') }}</span>
        </div>

        <h1 class="hero-title">
          {{ t('hero.title') }} <span class="gradient-text animate-gradient">Sirojbek</span>
        </h1>

        <h2 class="hero-subtitle">
          <span>{{ t('hero.subtitle') }}</span>
        </h2>

        <p class="hero-description">
          {{ t('hero.desc') }}
        </p>

        <div class="hero-actions">
          <a href="#projects" class="btn btn-primary">
            <span>{{ t('hero.cta_projects') }}</span>
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="5" y1="12" x2="19" y2="12"></line><polyline points="12 5 19 12 12 19"></polyline></svg>
          </a>
          <a href="#contact" class="btn btn-outline">{{ t('hero.cta_contact') }}</a>
        </div>

        <!-- Social Icons -->
        <div class="social-links">
          <a href="https://github.com/SirojbekMuxtorov2006" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="GitHub">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
          </a>
          <a href="https://t.me/sirojbekmuxtorov" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="Telegram">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M11.944 0A12 12 0 0 0 0 12a12 12 0 0 0 12 12 12 12 0 0 0 12-12A12 12 0 0 0 12 0a12 12 0 0 0-.056 0zm4.962 7.224c.1-.002.321.023.465.14a.506.506 0 0 1 .171.325c.016.093.036.306.02.472-.18 1.898-.962 6.502-1.36 8.627-.168.9-.499 1.201-.82 1.23-.696.065-1.225-.46-1.9-.902-1.056-.693-1.653-1.124-2.678-1.8-1.185-.78-.417-1.21.258-1.91.177-.184 3.247-2.977 3.307-3.23.007-.032.014-.15-.056-.212s-.174-.041-.249-.024c-.106.024-1.793 1.14-5.061 3.345-.48.33-.913.49-1.302.48-.428-.008-1.252-.241-1.865-.44-.752-.245-1.349-.374-1.297-.789.027-.216.325-.437.893-.663 3.498-1.524 5.83-2.529 6.998-3.014 3.332-1.386 4.025-1.627 4.476-1.635z"/></svg>
          </a>
          <a href="https://www.linkedin.com/in/sirojbek-muxtorov/" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="LinkedIn">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
          </a>
        </div>
      </div>
    </div>

    <!-- Scroll indicator -->
    <a href="#about" class="scroll-indicator" aria-label="Scroll to About">
      <div class="mouse">
        <div class="wheel"></div>
      </div>
      <div class="arrows">
        <span></span>
        <span></span>
      </div>
    </a>
  </section>
</template>

<style scoped>
.hero-section {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  overflow: hidden;
  background-color: var(--color-bg-primary);
  padding-top: 80px;
}

/* Background Animated Blobs */
.blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(120px);
  z-index: 1;
  opacity: 0.25;
  mix-blend-mode: screen;
}

.blob-1 {
  top: 10%;
  left: 10%;
  width: 400px;
  height: 400px;
  background: var(--color-accent-1);
  animation: float 18s infinite ease-in-out;
}

.blob-2 {
  bottom: 10%;
  right: 15%;
  width: 500px;
  height: 500px;
  background: var(--color-accent-2);
  animation: float 22s infinite ease-in-out alternate;
}

.blob-3 {
  top: 40%;
  left: 60%;
  width: 350px;
  height: 350px;
  background: var(--color-accent-3);
  animation: float 15s infinite ease-in-out 3s;
}

.dots-overlay {
  position: absolute;
  inset: 0;
  background-image: radial-gradient(rgba(255, 255, 255, 0.03) 1px, transparent 1px);
  background-size: 32px 32px;
  z-index: 2;
}

:root.light-mode .dots-overlay {
  background-image: radial-gradient(rgba(0, 0, 0, 0.05) 1px, transparent 1px);
}

.hero-container {
  position: relative;
  z-index: 3;
}

.hero-content {
  max-width: 800px;
  animation: slide-up 1s cubic-bezier(0.16, 1, 0.3, 1);
}

.greeting-badge {
  display: inline-flex;
  align-items: center;
  gap: var(--space-sm);
  background: var(--color-bg-glass);
  border: 1px solid var(--color-border-glass);
  padding: 0.5rem 1rem;
  border-radius: var(--radius-full);
  font-size: 0.85rem;
  font-weight: 600;
  margin-bottom: var(--space-xl);
}

.pulse-dot {
  width: 8px;
  height: 8px;
  background-color: #10b981;
  border-radius: 50%;
  box-shadow: 0 0 10px #10b981;
  animation: pulse-glow 2s infinite;
}

.hero-title {
  font-size: clamp(2.5rem, 8vw, 4.5rem);
  font-weight: 900;
  line-height: 1.1;
  letter-spacing: -0.04em;
  margin-bottom: var(--space-md);
}

.animate-gradient {
  background-size: 200% auto;
  animation: gradient-shift 6s linear infinite;
}

.hero-subtitle {
  font-size: clamp(1.2rem, 3vw, 1.8rem);
  font-weight: 600;
  margin-bottom: var(--space-lg);
  color: var(--color-accent-3);
  min-height: auto;
  letter-spacing: -0.01em;
  line-height: 1.3;
}

.hero-description {
  font-size: clamp(1.05rem, 2vw, 1.25rem);
  color: var(--color-text-secondary);
  line-height: 1.7;
  margin-bottom: var(--space-3xl);
  max-width: 650px;
}

.hero-actions {
  display: flex;
  gap: var(--space-lg);
  flex-wrap: wrap;
  margin-bottom: var(--space-4xl);
}

/* Button Component */
.btn {
  display: inline-flex;
  align-items: center;
  gap: var(--space-sm);
  padding: 1rem 2rem;
  border-radius: var(--radius-md);
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all var(--transition-base);
}

.btn-primary {
  background: var(--gradient-primary);
  color: #fff;
  border: none;
  position: relative;
  overflow: hidden;
  box-shadow: var(--shadow-glow);
}

.btn-primary::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transform: translateX(-100%);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-glow-lg);
}

.btn-primary:hover::after {
  animation: shimmer 1.5s infinite;
}

.btn-primary svg {
  transition: transform var(--transition-fast);
}

.btn-primary:hover svg {
  transform: translateX(4px);
}

.btn-outline {
  background: transparent;
  color: var(--color-text-primary);
  border: 1px solid var(--color-border-glass);
}

.btn-outline:hover {
  background: var(--color-bg-glass);
  border-color: var(--color-accent-3);
  transform: translateY(-3px);
  box-shadow: 0 0 20px rgba(6, 182, 212, 0.15);
}

/* Social links */
.social-links {
  display: flex;
  gap: var(--space-md);
}

.social-icon {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  background: var(--color-bg-glass);
  border: 1px solid var(--color-border-glass);
  color: var(--color-text-secondary);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all var(--transition-spring);
}

.social-icon:hover {
  color: var(--color-text-primary);
  transform: translateY(-5px) scale(1.1);
  border-color: var(--color-accent-1);
  box-shadow: var(--shadow-glow);
}

/* Scroll indicator */
.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: var(--space-xs);
  z-index: 10;
  opacity: 0.7;
  transition: opacity var(--transition-fast);
}

.scroll-indicator:hover {
  opacity: 1;
}

.mouse {
  width: 26px;
  height: 42px;
  border: 2px solid var(--color-text-secondary);
  border-radius: 20px;
  position: relative;
}

.wheel {
  width: 4px;
  height: 8px;
  background-color: var(--color-accent-3);
  border-radius: 2px;
  position: absolute;
  top: 8px;
  left: 50%;
  transform: translateX(-50%);
  animation: float 1.5s infinite ease-in-out;
}

.arrows {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.arrows span {
  display: block;
  width: 8px;
  height: 8px;
  border-bottom: 2px solid var(--color-text-muted);
  border-right: 2px solid var(--color-text-muted);
  transform: rotate(45deg);
  margin: -2px;
  animation: arrow-bounce 2s infinite;
}

.arrows span:nth-child(2) {
  animation-delay: 0.2s;
}

@keyframes arrow-bounce {
  0% {
    opacity: 0;
    transform: rotate(45deg) translate(-5px, -5px);
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: rotate(45deg) translate(5px, 5px);
  }
}

@media (max-width: 768px) {
  .hero-section {
    padding-top: 100px;
  }
  .hero-actions {
    gap: var(--space-md);
  }
  .btn {
    width: 100%;
    justify-content: center;
  }
}
</style>
