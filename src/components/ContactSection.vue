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
  }, 1200)
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
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" viewBox="0 0 256 256"><path d="M224,48H32a16,16,0,0,0-16,16V192a16,16,0,0,0,16,16H224a16,16,0,0,0,16-16V64A16,16,0,0,0,224,48ZM224,64l-96,64L32,64ZM32,192V82l90.66,60.44a8,8,0,0,0,8.68,0L224,82v110Z"></path></svg>
              </div>
              <div class="info-details">
                <span class="info-label">{{ t('contact.label_email') }}</span>
                <a href="mailto:sirojbekmuxtorov9@gmail.com" class="info-value">sirojbekmuxtorov9@gmail.com</a>
              </div>
            </div>

            <div class="info-item">
              <div class="info-icon">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" viewBox="0 0 256 256"><path d="M222.37,158.46l-47.11-21.11-.13-.06a16,16,0,0,0-15.17,1.4L137.9,155.1A102.94,102.94,0,0,1,100.9,118.1l16.4-22.09a16,16,0,0,0,1.4-15.17l-.06-.13L97.54,33.63a16,16,0,0,0-21-9.3L40.38,38.24A16,16,0,0,0,30,53.4C30,147.28,108.72,226,202.6,226a16,16,0,0,0,15.16-10.38l13.91-36.16A16,16,0,0,0,222.37,158.46ZM202.6,210c-85,0-156.6-71.6-156.6-156.6l36.16-13.91,21.11,47.11L86.84,108.69a8,8,0,0,0-.56,7.94,118.81,118.81,0,0,0,53.09,53.09,8,8,0,0,0,7.94-.56l22.09-16.4,47.11,21.11Z"></path></svg>
              </div>
              <div class="info-details">
                <span class="info-label">{{ t('contact.label_phone') }}</span>
                <a href="tel:+998901920755" class="info-value">+998 (90) 192-07-55</a>
              </div>
            </div>

            <div class="info-item">
              <div class="info-icon">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="currentColor" viewBox="0 0 256 256"><path d="M128,16a88.1,88.1,0,0,0-88,88c0,75.3,80,132.17,83.41,134.55a8,8,0,0,0,9.18,0C136,236.17,216,179.3,216,104A88.1,88.1,0,0,0,128,16Zm0,201.4C113.11,189.66,56,143.06,56,104a72,72,0,0,1,144,0C200,143.06,142.89,189.66,128,217.4ZM128,72a32,32,0,1,0,32,32A32,32,0,0,0,128,72Zm0,48a16,16,0,1,1,16-16A16,16,0,0,1,128,120Z"></path></svg>
              </div>
              <div class="info-details">
                <span class="info-label">{{ t('contact.label_address') }}</span>
                <span class="info-value">Samarkand, Uzbekistan</span>
              </div>
            </div>
          </div>

          <!-- Languages Box (Minimal Pastel layout) -->
          <div class="languages-box bento-card">
            <h4 class="languages-title">{{ t('contact.languages_title') }}</h4>
            <ul class="languages-list">
              <li>
                <span class="lang-tag pastel-red">UZ</span>
                <span>{{ t('contact.lang_uz') }}</span>
              </li>
              <li>
                <span class="lang-tag pastel-blue">EN</span>
                <span>{{ t('contact.lang_en') }}</span>
              </li>
              <li>
                <span class="lang-tag pastel-green">RU</span>
                <span>{{ t('contact.lang_ru') }}</span>
              </li>
            </ul>
          </div>
        </div>

        <!-- Contact Form -->
        <div class="contact-form-container bento-card">
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
                width="16" 
                height="16" 
                fill="currentColor" 
                viewBox="0 0 256 256"
              >
                <path d="M227.32,28.68a16,16,0,0,0-15.66-4.08l-180,60a16,16,0,0,0-3.51,29.24L101.49,154.5l41.15,73.16A16,16,0,0,0,156,236h1.72a16,16,0,0,0,13.79-11.83l60-180A16,16,0,0,0,227.32,28.68ZM156,220l-41.15-73.16a16,16,0,0,0-13.79-11.83L36,100l180-60L156,220Z"></path>
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
        <p class="footer-sub">Premium Utilitarian Minimalist UI</p>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.section-header {
  text-align: left;
  margin-bottom: var(--space-2xl);
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: var(--space-3xl);
  margin-bottom: var(--space-4xl);
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: var(--space-md);
}

.info-title {
  font-size: 1.4rem;
  font-weight: 800;
  letter-spacing: -0.01em;
  color: var(--color-text-primary);
}

.info-desc {
  color: var(--color-text-secondary);
  line-height: 1.6;
  font-size: 0.95rem;
}

.info-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-lg);
  margin-top: var(--space-md);
}

.info-item {
  display: flex;
  gap: var(--space-md);
  align-items: center;
}

.info-icon {
  width: 42px;
  height: 42px;
  border-radius: var(--radius-sm);
  background: var(--color-bg-secondary);
  border: 1px solid var(--color-border);
  color: var(--color-text-secondary);
  display: flex;
  align-items: center;
  justify-content: center;
}

.info-details {
  display: flex;
  flex-direction: column;
}

.info-label {
  font-size: 0.7rem;
  color: var(--color-text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-weight: 700;
}

.info-value {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--color-text-primary);
}

a.info-value:hover {
  text-decoration: underline;
}

/* Languages Box */
.languages-box {
  margin-top: var(--space-lg);
  padding: var(--space-lg);
}

.languages-title {
  font-size: 1rem;
  font-weight: 800;
  margin-bottom: var(--space-sm);
  color: var(--color-text-primary);
}

.languages-list {
  display: flex;
  flex-direction: column;
  gap: var(--space-xs);
}

.languages-list li {
  display: flex;
  align-items: center;
  gap: var(--space-md);
  font-size: 0.88rem;
  color: var(--color-text-secondary);
}

.lang-tag {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  font-weight: 700;
  padding: 0.15rem 0.45rem;
  border-radius: var(--radius-sm);
}

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

/* Form */
.contact-form-container {
  padding: var(--space-2xl);
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: var(--space-lg);
}

.input-group {
  position: relative;
  width: 100%;
}

.input-group input,
.input-group textarea {
  width: 100%;
  padding: 0.85rem;
  background: var(--color-bg-primary);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-sm);
  color: var(--color-text-primary);
  font-size: 0.95rem;
  font-family: inherit;
  outline: none;
  transition: all var(--transition-fast);
}

.input-group textarea {
  resize: none;
}

.input-group label {
  position: absolute;
  left: 0.85rem;
  top: 0.85rem;
  color: var(--color-text-muted);
  pointer-events: none;
  transition: all var(--transition-fast);
  font-size: 0.9rem;
}

.input-group input:focus ~ label,
.input-group input:not(:placeholder-shown) ~ label,
.input-group textarea:focus ~ label,
.input-group textarea:not(:placeholder-shown) ~ label {
  top: -0.6rem;
  left: 0.6rem;
  font-size: 0.75rem;
  color: var(--color-text-primary);
  background: var(--color-bg-secondary);
  padding-inline: 0.35rem;
  font-weight: 700;
}

.input-group input:focus,
.input-group textarea:focus {
  border-color: var(--color-text-primary);
}

.submit-btn {
  width: 100%;
  justify-content: center;
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.success-alert {
  padding: 0.75rem;
  border: 1px solid rgba(52, 101, 56, 0.2);
  background: var(--color-accent-green-bg);
  color: var(--color-accent-green-text);
  border-radius: var(--radius-sm);
  font-size: 0.85rem;
  font-weight: 600;
  text-align: center;
}

/* Footer styling */
.footer {
  margin-top: var(--space-4xl);
  padding-top: var(--space-lg);
  border-top: 1px solid var(--color-border);
  text-align: center;
  color: var(--color-text-muted);
  font-size: 0.85rem;
}

.footer-sub {
  font-size: 0.7rem;
  margin-top: var(--space-xs);
  color: var(--color-text-muted);
  letter-spacing: 0.05em;
  text-transform: uppercase;
  font-weight: 700;
}

@media (max-width: 992px) {
  .contact-grid {
    grid-template-columns: 1fr;
    gap: var(--space-2xl);
  }
}

@media (max-width: 576px) {
  .contact-form-container {
    padding: var(--space-lg);
  }
}

/* Transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity var(--transition-fast);
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
