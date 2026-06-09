<script setup>
import { ref, onMounted, onUnmounted, inject } from 'vue'

const t = inject('t')
const locale = inject('locale')
const theme = inject('theme')
const toggleTheme = inject('toggleTheme')
const changeLanguage = inject('changeLanguage')

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)
const isLangDropdownOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
  isLangDropdownOpen.value = false
}

const toggleLangDropdown = () => {
  isLangDropdownOpen.value = !isLangDropdownOpen.value
}

const selectLanguage = (lang) => {
  changeLanguage(lang)
  isLangDropdownOpen.value = false
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <nav :class="['navbar', { 'scrolled': isScrolled }]">
    <div class="container nav-container">
      <a href="#" class="logo" @click="closeMobileMenu">
        <span>Sirojbek.</span>
      </a>

      <!-- Desktop Links -->
      <ul class="nav-links">
        <li><a href="#about" class="nav-link">{{ t('nav.about') }}</a></li>
        <li><a href="#skills" class="nav-link">{{ t('nav.skills') }}</a></li>
        <li><a href="#projects" class="nav-link">{{ t('nav.projects') }}</a></li>
        <li><a href="#contact" class="nav-link">{{ t('nav.contact') }}</a></li>
      </ul>

      <!-- Toolbar -->
      <div class="nav-toolbar">
        <!-- Theme Toggle -->
        <button class="tool-btn theme-toggle" @click="toggleTheme" :aria-label="theme === 'dark' ? 'Light mode' : 'Dark mode'">
          <svg v-if="theme === 'dark'" xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" viewBox="0 0 256 256"><path d="M128,80a48,48,0,1,0,48,48A48.05,48.05,0,0,0,128,80Zm0,80a32,32,0,1,1,32-32A32,32,0,0,1,128,160Zm-8-120V24a8,8,0,0,1,16,0V40a8,8,0,0,1,-16,0Zm0,192v16a8,8,0,0,1,-16,0V232a8,8,0,0,1,16,0ZM62.06,50.75a8,8,0,0,1,0,11.31L50.75,73.37a8,8,0,0,1,-11.31,-11.31L50.75,50.75A8,8,0,0,1,62.06,50.75Zm143.19,143.19a8,8,0,0,1,0,11.31l-11.31,11.31a8,8,0,0,1,-11.31,-11.31l11.31,-11.31A8,8,0,0,1,205.25,193.94ZM40,128a8,8,0,0,1,8,-8H64a8,8,0,0,1,0,16H48A8,8,0,0,1,40,128Zm152,0a8,8,0,0,1,8,-8h16a8,8,0,0,1,0,16H200A8,8,0,0,1,192,128ZM62.06,205.25l-11.31,11.31a8,8,0,0,1,-11.31,-11.31l11.31,-11.31a8,8,0,0,1,11.31,11.31Zm143.19,-154.5a8,8,0,0,1,0,11.31L193.94,73.37a8,8,0,0,1,-11.31,-11.31l11.31,-11.31A8,8,0,0,1,205.25,50.75Z"></path></svg>
          <svg v-else xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" viewBox="0 0 256 256"><path d="M233.54,142.23a8,8,0,0,0,-8-1.84,92.08,92.08,0,0,1,-109.93,-109.93,8,8,0,0,0,-9.84,-9.84a108.14,108.14,0,1,0,129.61,129.61A8,8,0,0,0,233.54,142.23ZM128,220A92,92,0,1,1,220,128,92.1,92.1,0,0,1,128,220Z"></path></svg>
        </button>

        <!-- Language Dropdown -->
        <div class="lang-selector">
          <button class="tool-btn lang-btn" @click="toggleLangDropdown">
            <span class="lang-text">{{ locale.toUpperCase() }}</span>
            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="currentColor" viewBox="0 0 256 256"><path d="M213.66,101.66l-80,80a8,8,0,0,1,-11.32,0l-80,-80a8,8,0,0,1,11.32,-11.32L128,164.69l74.34,-74.35a8,8,0,0,1,11.32,11.32Z"></path></svg>
          </button>
          
          <transition name="fade-slide">
            <ul v-if="isLangDropdownOpen" class="lang-dropdown bento-card">
              <li :class="{ active: locale === 'uz' }" @click="selectLanguage('uz')">UZ</li>
              <li :class="{ active: locale === 'en' }" @click="selectLanguage('en')">EN</li>
              <li :class="{ active: locale === 'ru' }" @click="selectLanguage('ru')">RU</li>
            </ul>
          </transition>
        </div>

        <!-- Mobile Menu Toggle -->
        <button 
          :class="['hamburger', { 'active': isMobileMenuOpen }]" 
          @click="toggleMobileMenu"
          aria-label="Menu"
        >
          <span class="bar"></span>
          <span class="bar"></span>
        </button>
      </div>

      <!-- Mobile Menu -->
      <transition name="slide-fade">
        <ul v-if="isMobileMenuOpen" class="mobile-menu bento-card">
          <li><a href="#about" class="mobile-link" @click="closeMobileMenu">{{ t('nav.about') }}</a></li>
          <li><a href="#skills" class="mobile-link" @click="closeMobileMenu">{{ t('nav.skills') }}</a></li>
          <li><a href="#projects" class="mobile-link" @click="closeMobileMenu">{{ t('nav.projects') }}</a></li>
          <li><a href="#contact" class="mobile-link" @click="closeMobileMenu">{{ t('nav.contact') }}</a></li>
        </ul>
      </transition>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 65px;
  z-index: 1000;
  background: var(--color-bg-primary);
  border-bottom: 1px solid transparent;
  display: flex;
  align-items: center;
  transition: all var(--transition-base);
}

.navbar.scrolled {
  background: var(--color-bg-glass);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--color-border);
  height: 60px;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.logo {
  font-family: var(--font-serif);
  font-size: 1.4rem;
  font-weight: 400;
  color: var(--color-text-primary);
  letter-spacing: -0.02em;
}

.nav-links {
  display: flex;
  gap: var(--space-xl);
  margin-left: auto;
  margin-right: var(--space-2xl);
}

.nav-link {
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--color-text-secondary);
  transition: color var(--transition-fast);
  padding: var(--space-xs) 0;
  position: relative;
}

.nav-link:hover {
  color: var(--color-text-primary);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 1px;
  background-color: var(--color-text-primary);
  transition: width var(--transition-fast);
}

.nav-link:hover::after {
  width: 100%;
}

/* Toolbar */
.nav-toolbar {
  display: flex;
  align-items: center;
  gap: var(--space-sm);
}

.tool-btn {
  background: var(--color-bg-secondary);
  border: 1px solid var(--color-border);
  color: var(--color-text-primary);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.5rem;
  border-radius: var(--radius-sm);
  transition: all var(--transition-fast);
}

.tool-btn:hover {
  border-color: var(--color-border-hover);
  background: var(--color-bg-primary);
}

.lang-selector {
  position: relative;
}

.lang-btn {
  gap: 0.35rem;
  padding: 0.5rem 0.75rem;
}

.lang-text {
  font-size: 0.8rem;
  font-weight: 700;
  font-family: var(--font-mono);
}

.lang-dropdown {
  position: absolute;
  top: 100%;
  right: 0;
  margin-top: 4px;
  width: 80px;
  display: flex;
  flex-direction: column;
  padding: 4px;
  border-radius: var(--radius-sm);
  z-index: 1020;
}

.lang-dropdown li {
  padding: 6px 12px;
  font-size: 0.8rem;
  font-weight: 700;
  font-family: var(--font-mono);
  color: var(--color-text-secondary);
  cursor: pointer;
  border-radius: var(--radius-sm);
  transition: all var(--transition-fast);
  text-align: center;
}

.lang-dropdown li:hover,
.lang-dropdown li.active {
  background: var(--color-bg-primary);
  color: var(--color-text-primary);
}

/* Hamburger */
.hamburger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 1010;
  padding: 0.5rem;
  flex-direction: column;
  gap: 6px;
}

.bar {
  display: block;
  width: 20px;
  height: 1.5px;
  background-color: var(--color-text-primary);
  transition: all var(--transition-base);
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }

  .hamburger {
    display: flex;
  }

  .hamburger.active .bar:nth-child(1) {
    transform: translateY(4px) rotate(45deg);
  }

  .hamburger.active .bar:nth-child(2) {
    transform: translateY(-4px) rotate(-45deg);
  }

  .mobile-menu {
    position: absolute;
    top: 60px;
    right: var(--space-md);
    width: 200px;
    padding: var(--space-md);
    display: flex;
    flex-direction: column;
    gap: var(--space-md);
    z-index: 1005;
    border-radius: var(--radius-sm);
    box-shadow: var(--shadow-hover);
  }

  .mobile-link {
    font-size: 0.95rem;
    font-weight: 600;
    color: var(--color-text-secondary);
    display: block;
    padding: var(--space-xs) 0;
  }

  .mobile-link:hover {
    color: var(--color-text-primary);
  }
}

/* Transitions */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all var(--transition-fast);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all var(--transition-fast);
}

.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-5px);
}
</style>
