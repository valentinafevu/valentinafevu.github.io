<script setup>
import { inject } from 'vue'
const locale = inject('locale')

const ui = {
  es: {
    label: 'Contacto',
    heading: 'Trabajemos juntos.',
    sub: 'Abierta a nuevos proyectos y oportunidades.',
    exportBtn: 'Exportar como PDF',
    built: 'Diseñado y construido con Vue',
  },
  en: {
    label: 'Contact',
    heading: "Let's work together.",
    sub: 'Open to new projects and opportunities.',
    exportBtn: 'Export as PDF',
    built: 'Designed & built with Vue',
  },
}

const links = [
  { label: 'LinkedIn', href: 'https://linkedin.com/in/valentinafevu' },
  { label: 'GitHub', href: 'https://github.com/valentinafevu' },
  { label: 'Email', href: 'mailto:valentinafevu@gmail.com' },
]

function exportPDF() {
  window.print()
}
</script>

<template>
  <footer id="contact" class="section footer-section">
    <div class="container footer-inner">
      <div class="footer-left">
        <p class="section-label">{{ ui[locale].label }}</p>
        <h2 class="footer-heading">{{ ui[locale].heading }}</h2>
        <p class="footer-sub">{{ ui[locale].sub }}</p>

        <button class="btn-export no-print" @click="exportPDF">
          <svg width="14" height="14" viewBox="0 0 14 14" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
            <path d="M7 1v8M4 6l3 3 3-3"/>
            <path d="M1 10v1a2 2 0 002 2h8a2 2 0 002-2v-1"/>
          </svg>
          {{ ui[locale].exportBtn }}
        </button>
      </div>

      <div class="footer-right">
        <ul class="footer-links">
          <li v-for="link in links" :key="link.label">
            <a :href="link.href" target="_blank" rel="noopener" class="footer-link">
              {{ link.label }} ↗
            </a>
          </li>
        </ul>
      </div>
    </div>

    <div class="container footer-bottom">
      <span>© 2024 Valentina Fevu</span>
      <span class="footer-dot">·</span>
      <span>{{ ui[locale].built }}</span>
    </div>
  </footer>
</template>

<style scoped>
.footer-section {
  padding-top: 72px;
  padding-bottom: 48px;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 48px;
  margin-bottom: 48px;
}

.footer-heading {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(28px, 4vw, 42px);
  font-weight: 400;
  color: var(--text-900);
  letter-spacing: -0.02em;
  margin-bottom: 8px;
}

.footer-sub {
  font-size: 15px;
  font-weight: 300;
  color: var(--text-600);
  margin-bottom: 24px;
}

.btn-export {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  font-family: 'DM Sans', sans-serif;
  font-size: 13px;
  font-weight: 500;
  color: var(--text-600);
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 8px 16px;
  cursor: pointer;
  transition: border-color 0.2s, color 0.2s, box-shadow 0.2s;
}

.btn-export:hover {
  border-color: var(--accent);
  color: var(--accent);
  box-shadow: 0 2px 8px rgba(45, 90, 45, 0.1);
}

.footer-links {
  display: flex;
  flex-direction: column;
  gap: 8px;
  align-items: flex-end;
}

.footer-link {
  font-size: 15px;
  font-weight: 400;
  color: var(--text-600);
  transition: color 0.2s;
}

.footer-link:hover {
  color: var(--accent);
}

.footer-bottom {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  color: var(--text-400);
  padding-top: 24px;
  border-top: 1px solid var(--border);
}

.footer-dot { opacity: 0.5; }

@media (max-width: 640px) {
  .footer-inner { flex-direction: column; }
  .footer-links { align-items: flex-start; }
}
</style>
