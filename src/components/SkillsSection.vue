<script setup>
import { ref, onMounted, inject } from 'vue'

const t = inject('t')
const sectionRef = ref(null)
const activeCategory = ref('aiml')

const categories = ['aiml', 'backend', 'frontend', 'devops']

const skillsData = {
  aiml: [
    { name: 'PyTorch & TensorFlow', level: 90, desc: 'Model architectures, CNNs, model training & optimization', colorClass: 'pastel-red' },
    { name: 'NLP & LLMs', level: 85, desc: 'Transformers, LangChain, OpenAI APIs, Vector Embeddings', colorClass: 'pastel-red' },
    { name: 'Computer Vision', level: 80, desc: 'YOLO, OpenCV, image classification, target detection', colorClass: 'pastel-red' },
    { name: 'MLOps', level: 75, desc: 'MLflow, Weights & Biases, model version control, DVC', colorClass: 'pastel-red' },
    { name: 'Data Processing', level: 90, desc: 'pandas, NumPy, Polars, ETL pipelines, data visualization', colorClass: 'pastel-red' }
  ],
  backend: [
    { name: 'Python (FastAPI, Django)', level: 95, desc: 'REST APIs, Async programming, WebSockets, Celery', colorClass: 'pastel-blue' },
    { name: 'Node.js (NestJS, Express)', level: 85, desc: 'Microservices, JWT auth, WebSockets communication', colorClass: 'pastel-blue' },
    { name: 'Languages (Go, Rust, C++)', level: 75, desc: 'System-level and concurrent backend code', colorClass: 'pastel-blue' },
    { name: 'API Development', level: 90, desc: 'GraphQL, Event-Driven Architectures, REST endpoints', colorClass: 'pastel-blue' }
  ],
  frontend: [
    { name: 'React.js & Next.js', level: 85, desc: 'Hooks, React Query, Context, Tailwind, Server Components', colorClass: 'pastel-green' },
    { name: 'Vue.js & Nuxt.js', level: 90, desc: 'SPA/SSR rendering, Composition API, state management', colorClass: 'pastel-green' },
    { name: 'TypeScript & JavaScript', level: 90, desc: 'Strict typing, modern ES6+, DOM manipulation', colorClass: 'pastel-green' },
    { name: 'HTML5 & CSS3 / SCSS', level: 95, desc: 'Responsive design, layouts, smooth keyframe animations', colorClass: 'pastel-green' }
  ],
  devops: [
    { name: 'PostgreSQL & Redis', level: 90, desc: 'pgvector, database index optimization, cache layers', colorClass: 'pastel-yellow' },
    { name: 'Vector DBs (Weaviate, Pinecone)', level: 80, desc: 'Semantic search, similarity databases for AI', colorClass: 'pastel-yellow' },
    { name: 'Docker & Kubernetes', level: 85, desc: 'Containerization, cluster management, deployment', colorClass: 'pastel-yellow' },
    { name: 'CI/CD & Monitoring', level: 80, desc: 'GitHub Actions, Prometheus, Grafana, Sentry logs', colorClass: 'pastel-yellow' }
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

      <!-- Category Filter Tabs (Minimal Outline) -->
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

      <!-- Bento Box Feature Grid -->
      <div class="skills-display-container">
        <transition name="fade-slide" mode="out-in">
          <div :key="activeCategory" class="skills-grid">
            <div 
              v-for="(skill, index) in skillsData[activeCategory]" 
              :key="skill.name" 
              class="skill-card bento-card"
            >
              <div class="skill-info">
                <div class="skill-title-block">
                  <span :class="['dot-indicator', skill.colorClass]"></span>
                  <h3 class="skill-name">{{ skill.name }}</h3>
                </div>
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
  text-align: left;
  margin-bottom: var(--space-2xl);
}

/* Category Tabs */
.category-tabs {
  display: flex;
  justify-content: flex-start;
  gap: var(--space-sm);
  margin-bottom: var(--space-2xl);
  flex-wrap: wrap;
}

.category-tab-btn {
  padding: 0.6rem 1.2rem;
  border-radius: var(--radius-sm);
  background: var(--color-bg-secondary);
  border: 1px solid var(--color-border);
  color: var(--color-text-secondary);
  font-size: 0.85rem;
  font-weight: 700;
  cursor: pointer;
  transition: all var(--transition-fast);
}

.category-tab-btn:hover {
  color: var(--color-text-primary);
  border-color: var(--color-border-hover);
}

.category-tab-btn.active {
  background: var(--color-text-primary);
  color: var(--color-bg-secondary);
  border-color: transparent;
}

/* Grid Layout */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: var(--space-lg);
}

/* Card Styling */
.skill-card {
  padding: var(--space-xl);
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
  border-radius: var(--radius-md);
}

.skill-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.skill-title-block {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
}

.dot-indicator {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  flex-shrink: 0;
}

.pastel-red { background-color: var(--color-accent-red-text); }
.pastel-blue { background-color: var(--color-accent-blue-text); }
.pastel-green { background-color: var(--color-accent-green-text); }
.pastel-yellow { background-color: var(--color-accent-yellow-text); }

.skill-name {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--color-text-primary);
  letter-spacing: -0.01em;
}

.skill-level {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  color: var(--color-text-secondary);
  font-weight: 600;
}

.skill-progress-bg {
  width: 100%;
  height: 4px;
  background: var(--color-border);
  border-radius: var(--radius-full);
  overflow: hidden;
}

.skill-progress-fill {
  height: 100%;
  background: var(--color-text-primary);
  border-radius: var(--radius-full);
  width: 0;
  transition: width 1s cubic-bezier(0.16, 1, 0.3, 1);
}

.skill-desc {
  font-size: 0.85rem;
  color: var(--color-text-secondary);
  line-height: 1.5;
}

/* Vue Slide Transitions */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all var(--transition-fast);
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
