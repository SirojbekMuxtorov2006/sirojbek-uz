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

  const duration = 1200
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
        <!-- Left: Crisp Minimal Profile Frame -->
        <div class="profile-container">
          <div class="profile-card bento-card">
            <div class="mac-dots">
              <span></span>
              <span></span>
              <span></span>
            </div>
            <div class="avatar-inner">
              <img src="/sirojbek.jpg" alt="Sirojbek Muxtorov" class="profile-img" />
            </div>
          </div>
        </div>

        <!-- Right: Text Content -->
        <div class="about-content">
          <h2 class="section-title">
            {{ t('about.title') }}
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
            <div class="stat-card bento-card">
              <span class="stat-number">{{ experience }}+</span>
              <span class="stat-label">{{ t('about.stats.exp') }}</span>
            </div>
            <div class="stat-card bento-card">
              <span class="stat-number">{{ projects }}+</span>
              <span class="stat-label">{{ t('about.stats.projects') }}</span>
            </div>
            <div class="stat-card bento-card">
              <span class="stat-number">{{ clients }}+</span>
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
  gap: var(--space-3xl);
  align-items: center;
}

/* Profile container & card */
.profile-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.profile-card {
  width: min(100%, 340px);
  padding: 8px;
  background: var(--color-bg-secondary);
  border-radius: var(--radius-md);
  position: relative;
  display: flex;
  flex-direction: column;
}

.mac-dots {
  display: flex;
  gap: 6px;
  padding-bottom: 8px;
  padding-left: 4px;
}

.mac-dots span {
  width: 8px;
  height: 8px;
  background-color: var(--color-border);
  border-radius: 50%;
}

.avatar-inner {
  width: 100%;
  aspect-ratio: 1;
  border-radius: 4px;
  overflow: hidden;
  border: 1px solid var(--color-border);
}

.profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform var(--transition-slow);
}

.profile-card:hover .profile-img {
  transform: scale(1.02);
}

/* About content styling */
.about-content {
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
}

.about-text {
  font-size: 1rem;
  color: var(--color-text-secondary);
  line-height: 1.7;
}

.about-text.highlight {
  font-size: 1.15rem;
  font-weight: 500;
  color: var(--color-text-primary);
  border-left: 2px solid var(--color-text-primary);
  padding-left: var(--space-md);
  margin-bottom: var(--space-xs);
}

/* Stats Row */
.stats-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--space-md);
  margin-top: var(--space-lg);
}

.stat-card {
  padding: var(--space-lg) var(--space-sm);
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: var(--space-xs);
  border-radius: var(--radius-sm);
}

.stat-number {
  font-size: 1.8rem;
  font-weight: 800;
  font-family: var(--font-mono);
  color: var(--color-text-primary);
  line-height: 1.1;
}

.stat-label {
  font-size: 0.75rem;
  color: var(--color-text-secondary);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

@media (max-width: 992px) {
  .about-grid {
    grid-template-columns: 1fr;
    gap: var(--space-2xl);
  }

  .profile-container {
    order: -1;
  }
}

@media (max-width: 576px) {
  .stats-row {
    grid-template-columns: 1fr;
  }
}
</style>
