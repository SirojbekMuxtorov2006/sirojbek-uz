<script setup>
import { ref, onMounted, inject } from 'vue'

const t = inject('t')

const sectionRef = ref(null)
const name = ref('')
const email = ref('')
const message = ref('')
const isSending = ref(false)
const formSuccess = ref(false)

const handleSubmit = () => {
  if (!name.value || !email.value || !message.value) return

  isSending.value = true
  
  // Simulate API post
  setTimeout(() => {
    isSending.value = false
    formSuccess.value = true
    name.value = ''
    email.value = ''
    message.value = ''

    setTimeout(() => {
      formSuccess.value = false
    }, 5000)
  }, 1800)
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
  <section id="contact" class="section fade-in-section" ref="sectionRef">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">
          {{ t('contact.title') }}
        </h2>
        <p class="section-subtitle">
          {{ t('contact.subtitle') }}
        </p>
      </div>

      <div class="contact-grid">
        <!-- Contact Info & Languages -->
        <div class="contact-info">
          <h3 class="info-title">{{ t('contact.info_title') }}</h3>
          <p class="info-desc">
            {{ t('contact.info_desc') }}
          </p>

          <div class="info-list">
            <div class="info-item">
              <div class="info-icon">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path><polyline points="22,6 12,13 2,6"></polyline></svg>
              </div>
              <div class="info-details">
                <span class="info-label">{{ t('contact.label_email') }}</span>
                <a href="mailto:sirojbekmuxtorov9@gmail.com" class="info-value">sirojbekmuxtorov9@gmail.com</a>
              </div>
            </div>

            <div class="info-item">
              <div class="info-icon">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path></svg>
              </div>
              <div class="info-details">
                <span class="info-label">{{ t('contact.label_phone') }}</span>
                <a href="tel:+998901920755" class="info-value">+998 (90) 192-07-55</a>
              </div>
            </div>

            <div class="info-item">
              <div class="info-icon">
                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path><circle cx="12" cy="10" r="3"></circle></svg>
              </div>
              <div class="info-details">
                <span class="info-label">{{ t('contact.label_address') }}</span>
                <span class="info-value">Samarkand, Uzbekistan</span>
              </div>
            </div>
          </div>

          <!-- Languages Box -->
          <div class="languages-box glass-card">
            <h4 class="languages-title">{{ t('contact.languages_title') }}</h4>
            <ul class="languages-list">
              <li>
                <span class="lang-dot"></span>
                <span>{{ t('contact.lang_uz') }}</span>
              </li>
              <li>
                <span class="lang-dot"></span>
                <span>{{ t('contact.lang_en') }}</span>
              </li>
              <li>
                <span class="lang-dot"></span>
                <span>{{ t('contact.lang_ru') }}</span>
              </li>
            </ul>
          </div>
        </div>

        <!-- Contact Form -->
        <div class="contact-form-container glass-card">
          <form @submit.prevent="handleSubmit" class="contact-form">
            <div class="input-group">
              <input 
                type="text" 
                id="name" 
                v-model="name" 
                required 
                placeholder=" "
              />
              <label for="name">{{ t('contact.form.name') }}</label>
            </div>

            <div class="input-group">
              <input 
                type="email" 
                id="email" 
                v-model="email" 
                required 
                placeholder=" "
              />
              <label for="email">{{ t('contact.form.email') }}</label>
            </div>

            <div class="input-group">
              <textarea 
                id="message" 
                v-model="message" 
                required 
                placeholder=" "
                rows="5"
              ></textarea>
              <label for="message">{{ t('contact.form.message') }}</label>
            </div>

            <button 
              type="submit" 
              class="btn btn-primary submit-btn" 
              :disabled="isSending || formSuccess"
            >
              <span v-if="isSending">{{ t('contact.form.btn_sending') }}</span>
              <span v-else-if="formSuccess">{{ t('contact.form.btn_sent') }}</span>
              <span v-else>{{ t('contact.form.btn_send') }}</span>
              
              <svg 
                v-if="!isSending && !formSuccess"
                xmlns="http://www.w3.org/2000/svg" 
                width="18" 
                height="18" 
                viewBox="0 0 24 24" 
                fill="none" 
                stroke="currentColor" 
                stroke-width="2" 
                stroke-linecap="round" 
                stroke-linejoin="round"
              >
                <line x1="22" y1="2" x2="11" y2="13"></line>
                <polygon points="22 2 15 22 11 13 2 9 22 2"></polygon>
              </svg>
            </button>

            <!-- Alert -->
            <transition name="fade">
              <div v-if="formSuccess" class="success-alert">
                {{ t('contact.form.success') }}
              </div>
            </transition>
          </form>
        </div>
      </div>

      <!-- Footer -->
      <footer class="footer">
        <p>&copy; 2026 Sirojbek Muxtorov. Barcha huquqlar himoyalangan.</p>
        <p class="footer-sub">Premium portfolio yaratildi</p>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: var(--space-3xl);
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: var(--space-4xl);
  margin-bottom: var(--space-5xl);
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: var(--space-lg);
}

.info-title {
  font-size: 1.8rem;
  font-weight: 800;
  letter-spacing: -0.02em;
}

.info-desc {
  color: var(--color-text-secondary);
  line-height: 1.7;
}

.info-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-xl);
  margin-top: var(--space-lg);
}

.info-item {
  display: flex;
  gap: var(--space-md);
  align-items: center;
}

.info-icon {
  width: 50px;
  height: 50px;
  border-radius: var(--radius-md);
  background: var(--color-bg-glass);
  border: 1px solid var(--color-border-glass);
  color: var(--color-accent-3);
  display: flex;
  align-items: center;
  justify-content: center;
}

.info-details {
  display: flex;
  flex-direction: column;
}

.info-label {
  font-size: 0.8rem;
  color: var(--color-text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-weight: 600;
}

.info-value {
  font-size: 1.05rem;
  font-weight: 600;
  color: var(--color-text-primary);
  transition: color var(--transition-fast);
}

a.info-value:hover {
  color: var(--color-accent-3);
}

/* Languages Box */
.languages-box {
  margin-top: var(--space-xl);
  padding: var(--space-xl);
}

.languages-title {
  font-size: 1.2rem;
  font-weight: 700;
  margin-bottom: var(--space-md);
  color: var(--color-text-primary);
}

.languages-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-sm);
}

.languages-list li {
  display: flex;
  align-items: center;
  gap: var(--space-md);
  font-size: 0.95rem;
  color: var(--color-text-secondary);
}

.lang-dot {
  width: 6px;
  height: 6px;
  background-color: var(--color-accent-2);
  border-radius: 50%;
}

/* Form container */
.contact-form-container {
  padding: var(--space-3xl);
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: var(--space-xl);
}

.input-group {
  position: relative;
  width: 100%;
}

.input-group input,
.input-group textarea {
  width: 100%;
  padding: 1rem;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid var(--color-border-glass);
  border-radius: var(--radius-md);
  color: var(--color-text-primary);
  font-size: 1rem;
  font-family: inherit;
  outline: none;
  transition: all var(--transition-base);
}

.input-group textarea {
  resize: none;
}

.input-group label {
  position: absolute;
  left: 1rem;
  top: 1rem;
  color: var(--color-text-muted);
  pointer-events: none;
  transition: all var(--transition-base);
  font-size: 1rem;
}

/* Floating labels magic */
.input-group input:focus ~ label,
.input-group input:not(:placeholder-shown) ~ label,
.input-group textarea:focus ~ label,
.input-group textarea:not(:placeholder-shown) ~ label {
  top: -0.65rem;
  left: 0.8rem;
  font-size: 0.8rem;
  color: var(--color-accent-3);
  background: var(--color-bg-secondary);
  padding-inline: 0.5rem;
  border-radius: var(--radius-sm);
  font-weight: 600;
}

.input-group input:focus,
.input-group textarea:focus {
  border-color: var(--color-accent-3);
  box-shadow: 0 0 15px rgba(6, 182, 212, 0.1);
  background: rgba(255, 255, 255, 0.04);
}

.submit-btn {
  width: 100%;
  justify-content: center;
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}

.success-alert {
  padding: 1rem;
  background: rgba(16, 185, 129, 0.1);
  border: 1px solid rgba(16, 185, 129, 0.2);
  color: #10b981;
  border-radius: var(--radius-md);
  font-size: 0.95rem;
  font-weight: 500;
  text-align: center;
}

/* Footer styling */
.footer {
  margin-top: var(--space-5xl);
  padding-top: var(--space-xl);
  border-top: 1px solid var(--color-border-glass);
  text-align: center;
  color: var(--color-text-muted);
  font-size: 0.9rem;
}

.footer-sub {
  font-size: 0.75rem;
  margin-top: var(--space-xs);
  color: var(--color-text-muted);
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

@media (max-width: 992px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: var(--space-3xl);
  }
}

@media (max-width: 576px) {
  .contact-form-container {
    padding: var(--space-xl);
  }
}

/* Transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity var(--transition-base);
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
