<script setup>
defineProps({ locale: String })
defineEmits(['toggle-locale'])

const ui = {
  es: { me: 'Yo', work: 'Proyectos', contact: 'Contacto', export: 'Exportar' },
  en: { me: 'Me', work: 'Work', contact: 'Contact', export: 'Export' },
}
</script>

<template>
  <nav class="navbar no-print">
    <div class="nav-inner container">
      <a href="#me" class="nav-name">Vale Fevu</a>
      <div class="nav-links">
        <a href="#me">{{ ui[locale].me }}</a>
        <a href="#work">{{ ui[locale].work }}</a>
        <a href="#contact">{{ ui[locale].contact }}</a>
        <a href="#contact" class="nav-export">{{ ui[locale].export }} ↓</a>

        <div class="lang-toggle">
          <button :class="['lang-btn', { active: locale === 'es' }]" @click="$emit('toggle-locale')">ES</button>
          <span class="lang-sep">/</span>
          <button :class="['lang-btn', { active: locale === 'en' }]" @click="$emit('toggle-locale')">EN</button>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(237, 245, 237, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
}

.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 56px;
}

.nav-name {
  font-weight: 600;
  font-size: 15px;
  color: var(--accent);
  letter-spacing: -0.01em;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 28px;
}

.nav-links a {
  font-size: 14px;
  font-weight: 400;
  color: var(--text-600);
  transition: color 0.2s;
}

.nav-links a:hover {
  color: var(--accent);
}

.nav-export {
  font-size: 13px !important;
  color: var(--text-400) !important;
}

.nav-export:hover {
  color: var(--accent) !important;
}

.lang-toggle {
  display: flex;
  align-items: center;
  gap: 2px;
  background: var(--accent-light);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 3px 6px;
}

.lang-sep {
  font-size: 11px;
  color: var(--text-400);
}

.lang-btn {
  font-family: 'DM Sans', sans-serif;
  font-size: 12px;
  font-weight: 500;
  color: var(--text-400);
  background: none;
  border: none;
  padding: 2px 6px;
  border-radius: 20px;
  cursor: pointer;
  transition: background 0.15s, color 0.15s;
}

.lang-btn.active {
  background: var(--white);
  color: var(--accent);
}
</style>
