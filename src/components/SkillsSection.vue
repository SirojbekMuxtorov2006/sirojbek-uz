<script setup>
import { ref, onMounted, inject } from 'vue'

const t = inject('t')
const sectionRef = ref(null)
const activeCategory = ref('aiml')

const categories = ['aiml', 'backend', 'frontend', 'devops']

const skillsData = {
  aiml: [
    { name: 'PyTorch & TensorFlow', level: 90, desc: 'Model architectures, CNNs, model training & optimization' },
    { name: 'NLP & LLMs', level: 85, desc: 'Transformers, LangChain, OpenAI APIs, Vector Embeddings' },
    { name: 'Computer Vision', level: 80, desc: 'YOLO, OpenCV, image classification, target detection' },
    { name: 'MLOps', level: 75, desc: 'MLflow, Weights & Biases, model version control, DVC' },
    { name: 'Data Processing', level: 90, desc: 'pandas, NumPy, Polars, ETL pipelines, data visualization' }
  ],
  backend: [
    { name: 'Python (FastAPI, Django)', level: 95, desc: 'REST APIs, Async programming, WebSockets, Celery' },
    { name: 'Node.js (NestJS, Express)', level: 85, desc: 'Microservices, JWT auth, WebSockets communication' },
    { name: 'Languages (Go, Rust, C++)', level: 75, desc: 'System-level and concurrent backend code' },
    { name: 'API Development', level: 90, desc: 'GraphQL, Event-Driven Architectures, REST endpoints' }
  ],
  frontend: [
    { name: 'React.js & Next.js', level: 85, desc: 'Hooks, React Query, Context, Tailwind, Server Components' },
    { name: 'Vue.js & Nuxt.js', level: 90, desc: 'SPA/SSR rendering, Composition API, state management' },
    { name: 'TypeScript & JavaScript', level: 90, desc: 'Strict typing, modern ES6+, DOM manipulation' },
    { name: 'HTML5 & CSS3 / SCSS', level: 95, desc: 'Responsive design, layouts, smooth keyframe animations' }
  ],
  devops: [
    { name: 'PostgreSQL & Redis', level: 90, desc: 'pgvector, database index optimization, cache layers' },
    { name: 'Vector DBs (Weaviate, Pinecone)', level: 80, desc: 'Semantic search, similarity databases for AI' },
    { name: 'Docker & Kubernetes', level: 85, desc: 'Containerization, cluster management, deployment' },
    { name: 'CI/CD & Monitoring', level: 80, desc: 'GitHub Actions, Prometheus, Grafana, Sentry logs' }
  ]
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
})
</script>

<template>
  <section id="skills" class="section fade-in-section" ref="sectionRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">
          {{ t('skills.title') }}
        </h2>
        <p class="section-subtitle">
          {{ t('skills.subtitle') }}
        </p>
      </div>

      <!-- Category Filter Tabs -->
      <div class="category-tabs">
        <button 
          v-for="cat in categories" 
          :key="cat"
          :class="['category-tab-btn', { active: activeCategory === cat }]"
          @click="activeCategory = cat"
        >
          {{ t(`skills.categories.${cat}`) }}
        </button>
      </div>

      <!-- Skills Display Grid -->
      <div class="skills-display-container">
        <transition name="fade-slide" mode="out-in">
          <div :key="activeCategory" class="skills-grid">
            <div 
              v-for="(skill, index) in skillsData[activeCategory]" 
              :key="skill.name" 
              class="skill-card glass-card"
            >
              <div class="skill-info">
                <h3 class="skill-name">{{ skill.name }}</h3>
                <span class="skill-level">{{ skill.level }}%</span>
              </div>
              
              <div class="skill-progress-bg">
                <div class="skill-progress-fill" :style="{ width: skill.level + '%' }"></div>
              </div>

              <p class="skill-desc">{{ skill.desc }}</p>
            </div>
          </div>
        </transition>
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

/* Category Tabs */
.category-tabs {
  display: flex;
  justify-content: center;
  gap: var(--space-md);
  margin-bottom: var(--space-3xl);
  flex-wrap: wrap;
}

.category-tab-btn {
  padding: 0.8rem 1.6rem;
  border-radius: var(--radius-md);
  background: var(--color-bg-glass);
  border: 1px solid var(--color-border-glass);
  color: var(--color-text-secondary);
  font-weight: 700;
  cursor: pointer;
  transition: all var(--transition-base);
}

.category-tab-btn:hover {
  color: var(--color-text-primary);
  border-color: var(--color-accent-1);
}

.category-tab-btn.active {
  background: var(--gradient-primary);
  color: #fff;
  border-color: transparent;
  box-shadow: var(--shadow-glow);
}

/* Grid Layout */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: var(--space-xl);
}

/* Card Styling */
.skill-card {
  padding: var(--space-xl);
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
  transition: transform var(--transition-base), border-color var(--transition-base), box-shadow var(--transition-base);
}

.skill-card:hover {
  border-color: rgba(108, 92, 231, 0.3);
  transform: translateY(-4px);
  box-shadow: var(--shadow-glow);
}

.skill-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.skill-name {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--color-text-primary);
}

.skill-level {
  font-family: var(--font-mono);
  font-size: 0.95rem;
  color: var(--color-accent-3);
  font-weight: 600;
}

.skill-progress-bg {
  width: 100%;
  height: 6px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: var(--radius-full);
  overflow: hidden;
}

:root.light-mode .skill-progress-bg {
  background: rgba(0, 0, 0, 0.05);
}

.skill-progress-fill {
  height: 100%;
  background: var(--gradient-primary);
  border-radius: var(--radius-full);
  width: 0;
  transition: width 1s cubic-bezier(0.16, 1, 0.3, 1);
}

/* Trigger animation on visible state */
.fade-in-section.visible .skill-progress-fill {
  /* Dynamic style will apply the actual width, so this triggers transition */
}

.skill-desc {
  font-size: 0.9rem;
  color: var(--color-text-secondary);
  line-height: 1.5;
}

/* Vue Slide Transitions */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all var(--transition-base);
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
</style>
