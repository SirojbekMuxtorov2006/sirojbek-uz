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
  
  return list.filter(p => p.category === activeFilter.value)
})

const getTagColorClass = (tag) => {
  const lower = tag.toLowerCase()
  if (lower.includes('fastapi') || lower.includes('python') || lower.includes('ai') || lower.includes('openai')) return 'pastel-red'
  if (lower.includes('react') || lower.includes('next') || lower.includes('js') || lower.includes('ts')) return 'pastel-blue'
  if (lower.includes('vue') || lower.includes('pinia') || lower.includes('nuxt') || lower.includes('css')) return 'pastel-green'
  return 'pastel-yellow'
}

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

      <!-- Projects Bento Grid -->
      <div class="projects-grid">
        <transition-group name="project-list">
          <div 
            v-for="project in filteredProjects" 
            :key="project.title" 
            class="project-card bento-card"
          >
            <!-- Faux Mac Window Frame Chrome -->
            <div class="mac-frame">
              <div class="mac-dots">
                <span></span>
                <span></span>
                <span></span>
              </div>
              <span class="mac-title">{{ project.category }}</span>
            </div>

            <!-- Card Info -->
            <div class="project-info">
              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-desc">{{ project.desc }}</p>
              
              <div class="tags-container">
                <span 
                  v-for="tag in project.tags" 
                  :key="tag" 
                  :class="['tag', getTagColorClass(tag)]"
                >
                  {{ tag }}
                </span>
              </div>

              <!-- Inline Actions -->
              <div class="project-actions">
                <a href="https://github.com/SirojbekMuxtorov2006" target="_blank" class="action-btn">
                  <span>Demo</span>
                  <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="currentColor" viewBox="0 0 256 256"><path d="M221.66,133.66l-72,72a8,8,0,0,1-11.32-11.32L196.69,136H40a8,8,0,0,1,0-16H196.69L138.34,61.66a8,8,0,0,1,11.32-11.32l72,72A8,8,0,0,1,221.66,133.66Z"></path></svg>
                </a>
                <a href="https://github.com/SirojbekMuxtorov2006" target="_blank" class="action-btn">
                  <span>GitHub</span>
                  <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="currentColor" viewBox="0 0 256 256"><path d="M224,128a96,96,0,1,1-96-96A96,96,0,0,1,224,128Z" opacity="0.2"></path><path d="M208,104a80,80,0,0,0-160,0c0,34,18.84,63.63,47.16,79.43-1.86,4.69-3.79,9.45-5.83,14.2A12,12,0,0,0,80.37,213l29.47,11.8A12,12,0,0,0,125,217.43l3.66-22,3.66,22A12,12,0,0,0,146.16,224.8l29.47-11.8a12,12,0,0,0,11.05-19.41c-2-4.75-4-9.51-5.83-14.2A80.12,80.12,0,0,0,208,104Zm-80,98.2L116,128.2l-12,50.11v11.8L128,202.2Zm44-19.89L160,202.2l0-12.09,12-50.11ZM192,104a64,64,0,0,1-128,0c0-26.68,16.53-48,40-48s40,21.32,40,48S165.47,152,192,104Z"></path></svg>
                </a>
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
  text-align: left;
  margin-bottom: var(--space-2xl);
}

/* Filter buttons */
.filter-container {
  display: flex;
  justify-content: flex-start;
  gap: var(--space-sm);
  margin-bottom: var(--space-2xl);
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.5rem 1rem;
  border-radius: var(--radius-sm);
  background: var(--color-bg-secondary);
  border: 1px solid var(--color-border);
  color: var(--color-text-secondary);
  font-size: 0.85rem;
  font-weight: 700;
  cursor: pointer;
  transition: all var(--transition-fast);
}

.filter-btn:hover {
  color: var(--color-text-primary);
  border-color: var(--color-border-hover);
}

.filter-btn.active {
  background: var(--color-text-primary);
  color: var(--color-bg-secondary);
  border-color: transparent;
}

/* Grid Layout */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: var(--space-lg);
  position: relative;
}

/* Card Styling */
.project-card {
  display: flex;
  flex-direction: column;
  height: 100%;
  border-radius: var(--radius-md);
  background: var(--color-bg-secondary);
}

.mac-frame {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 16px;
  background: var(--color-bg-primary);
  border-bottom: 1px solid var(--color-border);
}

.mac-dots {
  display: flex;
  gap: 5px;
}

.mac-dots span {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background-color: var(--color-border-hover);
}

.mac-title {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  color: var(--color-text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.project-info {
  padding: var(--space-xl);
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
  flex-grow: 1;
}

.project-title {
  font-size: 1.15rem;
  font-weight: 800;
  letter-spacing: -0.01em;
  color: var(--color-text-primary);
}

.project-desc {
  font-size: 0.88rem;
  color: var(--color-text-secondary);
  line-height: 1.6;
}

.tags-container {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: auto;
  margin-bottom: var(--space-md);
}

.tag {
  padding: 0.25rem 0.65rem;
  border-radius: var(--radius-full);
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}

/* Localized Color overrides for Spot Pastels */
.pastel-red {
  background-color: var(--color-accent-red-bg);
  color: var(--color-accent-red-text);
}

.pastel-blue {
  background-color: var(--color-accent-blue-bg);
  color: var(--color-accent-blue-text);
}

.pastel-green {
  background-color: var(--color-accent-green-bg);
  color: var(--color-accent-green-text);
}

.pastel-yellow {
  background-color: var(--color-accent-yellow-bg);
  color: var(--color-accent-yellow-text);
}

/* Actions */
.project-actions {
  display: flex;
  gap: var(--space-md);
  border-top: 1px solid var(--color-border);
  padding-top: var(--space-md);
}

.action-btn {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  font-size: 0.8rem;
  font-weight: 700;
  color: var(--color-text-secondary);
  transition: color var(--transition-fast);
}

.action-btn:hover {
  color: var(--color-text-primary);
}

/* Vue List Transitions */
.project-list-enter-active,
.project-list-leave-active {
  transition: all 0.4s ease;
}

.project-list-enter-from {
  opacity: 0;
  transform: scale(0.97);
}

.project-list-leave-to {
  opacity: 0;
  transform: scale(0.97);
  position: absolute;
  width: 100%;
}
</style>
