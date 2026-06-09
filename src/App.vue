<script setup>
import { ref, onMounted, provide, watch } from 'vue'
import { translations } from './i18n'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'

// State for Language and Theme
const locale = ref(localStorage.getItem('portfolio-locale') || 'uz')
const theme = ref(localStorage.getItem('portfolio-theme') || 'dark')

// Translation helper
const t = (path) => {
  const keys = path.split('.')
  let current = translations[locale.value]
  for (const key of keys) {
    if (current && current[key] !== undefined) {
      current = current[key]
    } else {
      return path // Fallback to path key
    }
  }
  return current
}

const toggleTheme = () => {
  theme.value = theme.value === 'dark' ? 'light' : 'dark'
}

const changeLanguage = (lang) => {
  locale.value = lang
}

// Watchers to sync state with DOM and localStorage
watch(theme, (newTheme) => {
  localStorage.setItem('portfolio-theme', newTheme)
  const root = document.documentElement
  if (newTheme === 'light') {
    root.classList.add('light-mode')
  } else {
    root.classList.remove('light-mode')
  }
}, { immediate: true })

watch(locale, (newLocale) => {
  localStorage.setItem('portfolio-locale', newLocale)
})

// Provide translation context to all children
provide('t', t)
provide('locale', locale)
provide('theme', theme)
provide('toggleTheme', toggleTheme)
provide('changeLanguage', changeLanguage)

onMounted(() => {
  // IntersectionObserver to reveal elements on scroll
  const observerOptions = {
    root: null,
    rootMargin: '0px',
    threshold: 0.1
  }

  const observer = new IntersectionObserver((entries, observer) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
        observer.unobserve(entry.target)
      }
    })
  }, observerOptions)

  // Track all sections with .fade-in-section class
  const revealElements = document.querySelectorAll('.fade-in-section')
  revealElements.forEach(el => observer.observe(el))
})
</script>

<template>
  <div class="app-wrapper">
    <!-- Navigation Bar -->
    <NavBar />

    <!-- Hero Area -->
    <HeroSection />

    <!-- Main Content -->
    <main>
      <AboutSection />
      <SkillsSection />
      <ProjectsSection />
      <ContactSection />
    </main>
  </div>
</template>

<style>
/* App wrapper styling */
.app-wrapper {
  position: relative;
  min-height: 100vh;
  background-color: var(--color-bg-primary);
  overflow-x: hidden;
  transition: background-color var(--transition-base), color var(--transition-base);
}

main {
  position: relative;
  z-index: 5;
}
</style>
