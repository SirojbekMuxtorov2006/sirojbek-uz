<script setup>
import { inject } from 'vue'

const t = inject('t')
</script>

<template>
  <section class="hero-section">
    <!-- Subtle spotlight warm overlay -->
    <div class="spotlight"></div>
    <div class="grid-texture"></div>

    <div class="container hero-container">
      <div class="hero-content">
        <div class="greeting-badge">
          <span class="badge-dot"></span>
          <span class="badge-text">{{ t('hero.badge') }}</span>
        </div>

        <h1 class="hero-title">
          {{ t('hero.title') }} <span class="serif-name">Sirojbek.</span>
        </h1>

        <h2 class="hero-subtitle">
          {{ t('hero.subtitle') }}
        </h2>

        <p class="hero-description">
          {{ t('hero.desc') }}
        </p>

        <div class="hero-actions">
          <a href="#projects" class="btn btn-primary">
            <span>{{ t('hero.cta_projects') }}</span>
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 256 256"><path d="M221.66,133.66l-72,72a8,8,0,0,1-11.32-11.32L196.69,136H40a8,8,0,0,1,0-16H196.69L138.34,61.66a8,8,0,0,1,11.32-11.32l72,72A8,8,0,0,1,221.66,133.66Z"></path></svg>
          </a>
          <a href="#contact" class="btn btn-outline">{{ t('hero.cta_contact') }}</a>
        </div>

        <!-- Social Icons (Thick Stroke / Phosphor Style) -->
        <div class="social-links">
          <a href="https://github.com/SirojbekMuxtorov2006" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="GitHub">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" viewBox="0 0 256 256"><path d="M208,104a80,80,0,0,0-160,0c0,34,18.84,63.63,47.16,79.43-1.86,4.69-3.79,9.45-5.83,14.2A12,12,0,0,0,80.37,213l29.47,11.8A12,12,0,0,0,125,217.43l3.66-22,3.66,22A12,12,0,0,0,146.16,224.8l29.47-11.8a12,12,0,0,0,11.05-19.41c-2-4.75-4-9.51-5.83-14.2A80.12,80.12,0,0,0,208,104Zm-80,98.2L116,128.2l-12,50.11v11.8L128,202.2Zm44-19.89L160,202.2l0-12.09,12-50.11ZM192,104a64,64,0,0,1-128,0c0-26.68,16.53-48,40-48s40,21.32,40,48S165.47,152,192,104Z"></path></svg>
          </a>
          <a href="https://t.me/sirojbekmuxtorov" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="Telegram">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" viewBox="0 0 256 256"><path d="M236.88,26.19a9.63,9.63,0,0,0-9.67-.08L18.06,134.19a9.63,9.63,0,0,0,.14,17l60.13,29.43a8,8,0,0,0,9.08-1.57L198,89c1.9-1.9,3.8-3.8,1.9-5.7s-3.8,0-5.7,1.9L83.74,186a8,8,0,0,0-2.31,4.78l-7.79,46.73a9.63,9.63,0,0,0,15.65,8.53l35.84-29.46a8,8,0,0,0,4.78-2.31l72.23-72.23a9.63,9.63,0,0,0-5.26-15.68Z"></path></svg>
          </a>
          <a href="https://www.linkedin.com/in/sirojbek-muxtorov/" target="_blank" rel="noopener noreferrer" class="social-icon" aria-label="LinkedIn">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" viewBox="0 0 256 256"><path d="M224,40V216a16,16,0,0,1-16,16H48a16,16,0,0,1-16-16V40A16,16,0,0,1,48,24H208A16,16,0,0,1,224,40ZM96,96a8,8,0,0,0-16,0v80a8,8,0,0,0,16,0Zm-8-32a12,12,0,1,0-12-12A12,12,0,0,0,88,64Zm88,32c-15.42,0-25,8-28,13V96a8,8,0,0,0-16,0v80a8,8,0,0,0,16,0v-40c0-13,6-20,16-20s16,7,16,20v40a8,8,0,0,0,16,0V128C192,108,187.42,96,176,96Z"></path></svg>
          </a>
        </div>
      </div>
    </div>

    <!-- Scroll down indicator -->
    <a href="#about" class="scroll-indicator" aria-label="Scroll down">
      <div class="mouse">
        <span class="wheel"></span>
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
  border-bottom: 1px solid var(--color-border);
}

.spotlight {
  position: absolute;
  top: -10%;
  left: 50%;
  transform: translateX(-50%);
  width: 80vw;
  height: 60vh;
  background: radial-gradient(circle, rgba(230, 225, 215, 0.25) 0%, transparent 70%);
  z-index: 1;
  pointer-events: none;
}

:root.dark-mode .spotlight {
  background: radial-gradient(circle, rgba(40, 40, 40, 0.4) 0%, transparent 70%);
}

.grid-texture {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(var(--color-border) 1px, transparent 1px),
                    linear-gradient(90deg, var(--color-border) 1px, transparent 1px);
  background-size: 80px 80px;
  opacity: 0.15;
  z-index: 2;
  pointer-events: none;
}

.hero-container {
  position: relative;
  z-index: 3;
}

.hero-content {
  max-width: 760px;
  animation: slide-up 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.greeting-badge {
  display: inline-flex;
  align-items: center;
  gap: var(--space-sm);
  background: var(--color-accent-green-bg);
  border: 1px solid rgba(52, 101, 56, 0.15);
  padding: 0.4rem 0.8rem;
  border-radius: var(--radius-sm);
  margin-bottom: var(--space-lg);
}

.badge-dot {
  width: 6px;
  height: 6px;
  background-color: var(--color-accent-green-text);
  border-radius: 50%;
}

.badge-text {
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--color-accent-green-text);
}

.hero-title {
  font-size: clamp(3rem, 9vw, 5rem);
  font-weight: 800;
  line-height: 1.05;
  letter-spacing: -0.03em;
  margin-bottom: var(--space-sm);
  color: var(--color-text-primary);
}

.serif-name {
  font-family: var(--font-serif);
  font-weight: 400;
  font-style: italic;
}

.hero-subtitle {
  font-family: var(--font-mono);
  font-size: clamp(1rem, 2vw, 1.2rem);
  font-weight: 500;
  color: var(--color-text-secondary);
  margin-bottom: var(--space-lg);
}

.hero-description {
  font-size: clamp(1.05rem, 1.8vw, 1.15rem);
  color: var(--color-text-secondary);
  line-height: 1.7;
  margin-bottom: var(--space-2xl);
}

.hero-actions {
  display: flex;
  gap: var(--space-md);
  flex-wrap: wrap;
  margin-bottom: var(--space-3xl);
}

/* Button */
.btn {
  display: inline-flex;
  align-items: center;
  gap: var(--space-sm);
  padding: 0.85rem 1.75rem;
  border-radius: var(--radius-sm);
  font-weight: 700;
  font-size: 0.9rem;
  cursor: pointer;
  transition: all var(--transition-fast);
}

.btn-primary {
  background: var(--color-text-primary);
  color: var(--color-bg-secondary);
  border: none;
}

.btn-primary:hover {
  background: #333;
  transform: scale(0.98);
}

:root.dark-mode .btn-primary:hover {
  background: #ccc;
}

.btn-outline {
  background: transparent;
  color: var(--color-text-primary);
  border: 1px solid var(--color-border);
}

.btn-outline:hover {
  border-color: var(--color-border-hover);
  background: var(--color-bg-secondary);
  transform: scale(0.98);
}

/* Social links */
.social-links {
  display: flex;
  gap: var(--space-md);
}

.social-icon {
  width: 40px;
  height: 40px;
  border-radius: var(--radius-sm);
  background: var(--color-bg-secondary);
  border: 1px solid var(--color-border);
  color: var(--color-text-secondary);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all var(--transition-fast);
}

.social-icon:hover {
  color: var(--color-text-primary);
  border-color: var(--color-border-hover);
  transform: translateY(-2px);
}

/* Scroll indicator */
.scroll-indicator {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0.5;
  transition: opacity var(--transition-fast);
  z-index: 5;
}

.scroll-indicator:hover {
  opacity: 0.9;
}

.mouse {
  width: 20px;
  height: 32px;
  border: 1.5px solid var(--color-text-muted);
  border-radius: 10px;
  position: relative;
  display: block;
}

.wheel {
  width: 3px;
  height: 6px;
  background-color: var(--color-text-primary);
  border-radius: 2px;
  position: absolute;
  top: 6px;
  left: 50%;
  transform: translateX(-50%);
  animation: scroll-wheel 1.8s infinite ease-in-out;
}

@keyframes scroll-wheel {
  0% { transform: translate(-50%, 0); opacity: 0; }
  30% { opacity: 1; }
  100% { transform: translate(-50%, 8px); opacity: 0; }
}

@media (max-width: 576px) {
  .hero-actions {
    width: 100%;
  }
  .btn {
    width: 100%;
    justify-content: center;
  }
}
</style>
