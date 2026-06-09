<script setup>
import { ref, onMounted, inject } from 'vue'

const t = inject('t')

const experience = ref(0)
const projects = ref(0)
const clients = ref(0)
const sectionRef = ref(null)
const animated = ref(false)

const animateStats = () => {
  if (animated.value) return
  animated.value = true

  const targetExp = 3
  const targetProj = 50
  const targetClients = 30

  const duration = 1500
  const stepTime = 30

  let currentExp = 0
  let currentProj = 0
  let currentClients = 0

  const timer = setInterval(() => {
    currentExp += targetExp / (duration / stepTime)
    currentProj += targetProj / (duration / stepTime)
    currentClients += targetClients / (duration / stepTime)

    experience.value = Math.min(Math.floor(currentExp), targetExp)
    projects.value = Math.min(Math.floor(currentProj), targetProj)
    clients.value = Math.min(Math.floor(currentClients), targetClients)

    if (experience.value >= targetExp && projects.value >= targetProj && clients.value >= targetClients) {
      clearInterval(timer)
      experience.value = targetExp
      projects.value = targetProj
      clients.value = targetClients
    }
  }, stepTime)
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
        animateStats()
      }
    })
  }, { threshold: 0.15 })

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})
</script>

<template>
  <section id="about" class="section fade-in-section" ref="sectionRef">
    <div class="container">
      <div class="about-grid">
        <!-- Left: Image Frame with animated border -->
        <div class="profile-container">
          <div class="profile-card">
            <div class="avatar-glow"></div>
            <div class="avatar-frame">
              <div class="avatar-inner">
                <img src="/sirojbek.jpg" alt="Sirojbek Muxtorov" class="profile-img" />
              </div>
            </div>
          </div>
        </div>

        <!-- Right: Text Content -->
        <div class="about-content">
          <h2 class="section-title">
            <span class="gradient-text">{{ t('about.title') }}</span>
          </h2>
          <p class="about-text highlight">
            {{ t('about.highlight') }}
          </p>
          <p class="about-text">
            {{ t('about.p1') }}
          </p>
          <p class="about-text">
            {{ t('about.p2') }}
          </p>

          <!-- Stats Row -->
          <div class="stats-row">
            <div class="stat-card glass-card">
              <span class="stat-number gradient-text">{{ experience }}+</span>
              <span class="stat-label">{{ t('about.stats.exp') }}</span>
            </div>
            <div class="stat-card glass-card">
              <span class="stat-number gradient-text">{{ projects }}+</span>
              <span class="stat-label">{{ t('about.stats.projects') }}</span>
            </div>
            <div class="stat-card glass-card">
              <span class="stat-number gradient-text">{{ clients }}+</span>
              <span class="stat-label">{{ t('about.stats.clients') }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: var(--space-4xl);
  align-items: center;
}

/* Profile container & card */
.profile-container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.profile-card {
  position: relative;
  width: min(100%, 340px);
  aspect-ratio: 1;
}

.avatar-glow {
  position: absolute;
  inset: -10px;
  background: var(--gradient-primary);
  border-radius: var(--radius-xl);
  filter: blur(25px);
  opacity: 0.4;
  z-index: 1;
  animation: pulse-glow 3s infinite alternate;
}

.avatar-frame {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: var(--radius-xl);
  padding: 4px;
  background: var(--gradient-primary);
  background-size: 200% 200%;
  animation: gradient-shift 6s ease infinite;
  z-index: 2;
  box-shadow: var(--shadow-elevated);
}

.avatar-inner {
  width: 100%;
  height: 100%;
  background: var(--color-bg-secondary);
  border-radius: calc(var(--radius-xl) - 2px);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
}

.avatar-inner::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle, rgba(108, 92, 231, 0.1) 0%, transparent 70%);
}

.profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--transition-slow);
}

.profile-card:hover .profile-img {
  transform: scale(1.05);
}

/* About content styling */
.about-content {
  display: flex;
  flex-direction: column;
  gap: var(--space-lg);
}

.about-text {
  font-size: 1.05rem;
  color: var(--color-text-secondary);
  line-height: 1.8;
}

.about-text.highlight {
  font-size: 1.2rem;
  font-weight: 500;
  color: var(--color-text-primary);
  border-left: 3px solid var(--color-accent-1);
  padding-left: var(--space-md);
  margin-bottom: var(--space-xs);
}

/* Stats Row */
.stats-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--space-md);
  margin-top: var(--space-xl);
}

.stat-card {
  padding: var(--space-lg) var(--space-md);
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: var(--space-xs);
}

.stat-number {
  font-size: clamp(1.8rem, 3.5vw, 2.5rem);
  font-weight: 800;
  letter-spacing: -0.02em;
  line-height: 1.1;
}

.stat-label {
  font-size: 0.85rem;
  color: var(--color-text-secondary);
  font-weight: 500;
}

@media (max-width: 992px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: var(--space-3xl);
  }

  .profile-container {
    order: -1;
  }
}

@media (max-width: 576px) {
  .stats-row {
    grid-template-columns: 1fr;
  }
  .stat-card {
    padding: var(--space-md);
  }
}
</style>
