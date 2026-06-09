<script setup>
import { ref, computed, onMounted, inject } from 'vue'

const t = inject('t')

const sectionRef = ref(null)
const activeFilter = ref('Hammasi')

const filterKeys = ['all', 'backend', 'frontend', 'fullstack']

const filteredProjects = computed(() => {
  const list = t('projects.list')
  if (!Array.isArray(list)) return []
  
  if (activeFilter.value === 'Hammasi' || activeFilter.value === 'All' || activeFilter.value === 'Все') {
    return list
  }
  
  return list.filter(p => {
    // Matches localized categories
    return p.category === activeFilter.value
  })
})

const setFilter = (key) => {
  activeFilter.value = t(`projects.filters.${key}`)
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
      }
    })
  }, { threshold: 0.15 })

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
  
  // Set initial filter based on UZ translation
  activeFilter.value = t('projects.filters.all')
})
</script>

<template>
  <section id="projects" class="section fade-in-section" ref="sectionRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">
          {{ t('projects.title') }}
        </h2>
        <p class="section-subtitle">
          {{ t('projects.subtitle') }}
        </p>
      </div>

      <!-- Filters -->
      <div class="filter-container">
        <button 
          v-for="key in filterKeys" 
          :key="key"
          :class="['filter-btn', { active: activeFilter === t(`projects.filters.${key}`) }]"
          @click="setFilter(key)"
        >
          {{ t(`projects.filters.${key}`) }}
        </button>
      </div>

      <!-- Projects Grid -->
      <div class="projects-grid">
        <transition-group name="project-list">
          <div 
            v-for="project in filteredProjects" 
            :key="project.title" 
            class="project-card glass-card"
          >
            <!-- Image Area with customizable gradient fallback -->
            <div class="project-image" :style="{ background: project.gradient }">
              <div class="project-overlay">
                <div class="overlay-actions">
                  <a href="https://github.com/SirojbekMuxtorov2006" target="_blank" class="overlay-btn" aria-label="Live Demo">
                    <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path><polyline points="15 3 21 3 21 9"></polyline><line x1="10" y1="14" x2="21" y2="3"></line></svg>
                  </a>
                  <a href="https://github.com/SirojbekMuxtorov2006" target="_blank" class="overlay-btn" aria-label="GitHub Repository">
                    <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
                  </a>
                </div>
              </div>
              <div class="project-tag-badge">{{ project.category }}</div>
            </div>

            <!-- Card Info -->
            <div class="project-info">
              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-desc">{{ project.desc }}</p>
              
              <div class="tags-container">
                <span v-for="tag in project.tags" :key="tag" class="tag">
                  {{ tag }}
                </span>
              </div>
            </div>
          </div>
        </transition-group>
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: var(--space-2xl);
}

/* Filter buttons */
.filter-container {
  display: flex;
  justify-content: center;
  gap: var(--space-md);
  margin-bottom: var(--space-3xl);
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.6rem 1.4rem;
  border-radius: var(--radius-full);
  background: var(--color-bg-glass);
  border: 1px solid var(--color-border-glass);
  color: var(--color-text-secondary);
  font-weight: 600;
  cursor: pointer;
  transition: all var(--transition-base);
}

.filter-btn:hover {
  color: var(--color-text-primary);
  border-color: var(--color-accent-1);
}

.filter-btn.active {
  background: var(--gradient-primary);
  color: #fff;
  border-color: transparent;
  box-shadow: var(--shadow-glow);
}

/* Grid Layout */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: var(--space-2xl);
  position: relative;
}

/* Card Styling */
.project-card {
  display: flex;
  flex-direction: column;
  height: 100%;
  transition: transform var(--transition-base), border-color var(--transition-base), box-shadow var(--transition-base);
}

.project-image {
  height: 220px;
  width: 100%;
  position: relative;
  overflow: hidden;
  border-top-left-radius: inherit;
  border-top-right-radius: inherit;
}

.project-overlay {
  position: absolute;
  inset: 0;
  background: rgba(10, 10, 15, 0.85);
  backdrop-filter: blur(4px);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity var(--transition-base);
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.overlay-actions {
  display: flex;
  gap: var(--space-lg);
  transform: translateY(20px);
  transition: transform var(--transition-base);
}

.project-card:hover .overlay-actions {
  transform: translateY(0);
}

.overlay-btn {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: var(--gradient-primary);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform var(--transition-spring), box-shadow var(--transition-base);
  box-shadow: var(--shadow-glow);
}

.overlay-btn:hover {
  transform: scale(1.15);
  box-shadow: var(--shadow-glow-lg);
}

.project-tag-badge {
  position: absolute;
  top: var(--space-md);
  right: var(--space-md);
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 0.35rem 0.85rem;
  border-radius: var(--radius-full);
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--color-text-primary);
}

.project-info {
  padding: var(--space-xl);
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
  flex-grow: 1;
}

.project-title {
  font-size: 1.3rem;
  font-weight: 700;
  letter-spacing: -0.01em;
}

.project-desc {
  font-size: 0.95rem;
  color: var(--color-text-secondary);
  line-height: 1.6;
}

.tags-container {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-sm);
  margin-top: auto;
}

.tag {
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid var(--color-border-glass);
  padding: 0.25rem 0.75rem;
  border-radius: var(--radius-sm);
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--color-text-secondary);
}

/* Vue List Transitions */
.project-list-enter-active,
.project-list-leave-active {
  transition: all 0.5s ease;
}

.project-list-enter-from {
  opacity: 0;
  transform: scale(0.9);
}

.project-list-leave-to {
  opacity: 0;
  transform: scale(0.9);
  position: absolute;
  width: 100%;
}
</style>
