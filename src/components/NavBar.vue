<script setup>
import { ref, onMounted, onUnmounted, inject } from 'vue'

// Inject state from parent
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
        <span class="gradient-text">Sirojbek</span>
      </a>

      <!-- Desktop Links -->
      <ul class="nav-links">
        <li><a href="#about" class="nav-link">{{ t('nav.about') }}</a></li>
        <li><a href="#skills" class="nav-link">{{ t('nav.skills') }}</a></li>
        <li><a href="#projects" class="nav-link">{{ t('nav.projects') }}</a></li>
        <li><a href="#contact" class="nav-link">{{ t('nav.contact') }}</a></li>
      </ul>

      <!-- Toolbar: Theme and Language -->
      <div class="nav-toolbar">
        <!-- Theme Switcher -->
        <button class="tool-btn theme-toggle" @click="toggleTheme" :aria-label="theme === 'dark' ? 'Light mode' : 'Dark mode'">
          <!-- Sun Icon (visible in Dark Mode) -->
          <svg v-if="theme === 'dark'" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="5"></circle><line x1="12" y1="1" x2="12" y2="3"></line><line x1="12" y1="21" x2="12" y2="23"></line><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line><line x1="1" y1="12" x2="3" y2="12"></line><line x1="21" y1="12" x2="23" y2="12"></line><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line></svg>
          <!-- Moon Icon (visible in Light Mode) -->
          <svg v-else xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path></svg>
        </button>

        <!-- Language Dropdown Selector -->
        <div class="lang-selector">
          <button class="tool-btn lang-btn" @click="toggleLangDropdown">
            <span class="lang-text">{{ locale.toUpperCase() }}</span>
            <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 12 15 18 9"></polyline></svg>
          </button>
          
          <transition name="fade-slide">
            <ul v-if="isLangDropdownOpen" class="lang-dropdown glass-card">
              <li :class="{ active: locale === 'uz' }" @click="selectLanguage('uz')">UZ</li>
              <li :class="{ active: locale === 'en' }" @click="selectLanguage('en')">EN</li>
              <li :class="{ active: locale === 'ru' }" @click="selectLanguage('ru')">RU</li>
            </ul>
          </transition>
        </div>

        <!-- Hamburger Button -->
        <button 
          :class="['hamburger', { 'active': isMobileMenuOpen }]" 
          @click="toggleMobileMenu"
          aria-label="Menu"
        >
          <span class="bar"></span>
          <span class="bar"></span>
          <span class="bar"></span>
        </button>
      </div>

      <!-- Mobile Menu -->
      <transition name="slide-fade">
        <ul v-if="isMobileMenuOpen" class="mobile-menu glass-card">
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
  height: 75px;
  z-index: 1000;
  transition: all var(--transition-base);
  border-bottom: 1px solid transparent;
  display: flex;
  align-items: center;
}

.navbar.scrolled {
  background: var(--color-bg-glass);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--color-border-glass);
  height: 65px;
  box-shadow: var(--shadow-card);
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.logo {
  font-size: 1.5rem;
  font-weight: 800;
  letter-spacing: -0.03em;
  text-decoration: none;
}

.nav-links {
  display: flex;
  gap: var(--space-xl);
  margin-left: auto;
  margin-right: var(--space-2xl);
}

.nav-link {
  font-size: 0.95rem;
  font-weight: 500;
  color: var(--color-text-secondary);
  transition: color var(--transition-fast);
  position: relative;
  padding-block: var(--space-sm);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--gradient-primary);
  transition: width var(--transition-base);
  border-radius: var(--radius-full);
}

.nav-link:hover {
  color: var(--color-text-primary);
}

.nav-link:hover::after {
  width: 100%;
}

/* Nav Toolbar */
.nav-toolbar {
  display: flex;
  align-items: center;
  gap: var(--space-md);
}

.tool-btn {
  background: var(--color-bg-glass);
  border: 1px solid var(--color-border-glass);
  color: var(--color-text-primary);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.6rem;
  border-radius: var(--radius-md);
  transition: all var(--transition-fast);
}

.tool-btn:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: var(--color-accent-1);
  transform: translateY(-2px);
}

.lang-selector {
  position: relative;
}

.lang-btn {
  gap: var(--space-xs);
  padding: 0.6rem 0.9rem;
}

.lang-text {
  font-size: 0.85rem;
  font-weight: 700;
  font-family: var(--font-mono);
}

.lang-dropdown {
  position: absolute;
  top: 100%;
  right: 0;
  margin-top: var(--space-xs);
  width: 80px;
  display: flex;
  flex-direction: column;
  box-shadow: var(--shadow-elevated);
  padding: var(--space-xs);
  border-radius: var(--radius-md);
  z-index: 1020;
}

.lang-dropdown li {
  padding: var(--space-sm) var(--space-md);
  font-size: 0.85rem;
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
  background: var(--gradient-primary);
  color: #fff;
}

/* Hamburger */
.hamburger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 1010;
  padding: var(--space-sm);
}

.bar {
  display: block;
  width: 25px;
  height: 2px;
  margin: 5px auto;
  background-color: var(--color-text-primary);
  transition: all var(--transition-base);
  border-radius: var(--radius-full);
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }

  .hamburger {
    display: block;
  }

  .hamburger.active .bar:nth-child(2) {
    opacity: 0;
  }

  .hamburger.active .bar:nth-child(1) {
    transform: translateY(7px) rotate(45deg);
    background: var(--color-accent-1);
  }

  .hamburger.active .bar:nth-child(3) {
    transform: translateY(-7px) rotate(-45deg);
    background: var(--color-accent-1);
  }

  .mobile-menu {
    position: absolute;
    top: 70px;
    right: var(--space-md);
    width: calc(100vw - 2 * var(--space-md));
    padding: var(--space-xl);
    display: flex;
    flex-direction: column;
    gap: var(--space-lg);
    box-shadow: var(--shadow-elevated);
    z-index: 1005;
  }

  .mobile-link {
    font-size: 1.1rem;
    font-weight: 600;
    color: var(--color-text-secondary);
    display: block;
    padding-block: var(--space-xs);
    transition: color var(--transition-fast), transform var(--transition-fast);
  }

  .mobile-link:hover {
    color: var(--color-text-primary);
    transform: translateX(8px);
  }
}

/* Transitions */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all var(--transition-base);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all var(--transition-fast);
}

.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
