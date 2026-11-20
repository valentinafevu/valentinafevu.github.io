<script setup>
import { inject } from 'vue'
const locale = inject('locale')

const ui = {
  es: {
    label: 'Sobre mí',
    role: 'AI Engineer · ML Engineer · MsC Mathematics',
    bio: 'Construyo soluciones de IA aplicadas a moda y datos. Mi trabajo conecta visión por computadora, agentes de IA y análisis de datos para resolver problemas reales — desde sistemas de recomendación personalizados hasta investigación sobre transformers visuales. Me importa que la tecnología sea útil, clara y bien diseñada.',
    eduLabel: 'Educación',
    edu: [
      {
        degree: 'Maestría en Matemáticas',
        school: 'Pontificia Universidad Javeriana',
        period: '2024 – presente',
        badge: 'En curso',
        detail: 'Escribe aquí en qué te estás enfocando — tesis, línea de investigación, etc.',
      },
      {
        degree: 'Pregrado en Ingeniería de Sistemas y Computación',
        school: 'Pontificia Universidad Javeriana',
        period: '2016 – 2020',
        badge: null,
        detail: 'Énfasis en construcción de software. Escribe aquí más detalle sobre tu enfoque, proyectos de grado, o logros relevantes.',
      },
    ],
    skillLabels: { ai: 'IA / ML', dev: 'Desarrollo', tools: 'Herramientas' },
  },
  en: {
    label: 'About',
    role: 'AI Engineer · Data Analysis · Product Design',
    bio: 'I build AI solutions applied to fashion and data. My work connects computer vision, AI agents, and data analysis to solve real problems — from personalized recommendation systems to research on vision transformers. I care about technology being useful, clear, and well designed.',
    eduLabel: 'Education',
    edu: [
      {
        degree: "Master's in Mathematics",
        school: 'Pontificia Universidad Javeriana',
        period: '2024 – present',
        badge: 'In progress',
        detail: 'Write your focus here — thesis topic, research line, etc.',
      },
      {
        degree: "Bachelor's in Systems and Computing Engineering",
        school: 'Pontificia Universidad Javeriana',
        period: '2016 – 2020',
        badge: null,
        detail: 'Emphasis on software construction. Write more detail about your focus, thesis project, or relevant achievements.',
      },
    ],
    skillLabels: { ai: 'AI / ML', dev: 'Development', tools: 'Tools' },
  },
}

const skills = {
  ai: ['AI Agents', 'Computer Vision', 'Vision Transformers', 'RAG', 'MCP', 'Claude API'],
  dev: ['Python', 'PyTorch', 'Vue.js', 'SQL', 'Plotly', 'Jupyter'],
  tools: ['Figma', 'Git', 'Notion', 'Miro'],
}
</script>

<template>
  <section id="me" class="section hero-section">
    <div class="container">
      <div class="hero-top">
        <p class="section-label">{{ ui[locale].label }}</p>
        <h1 class="hero-name">Valentina Feruere</h1>
        <p class="hero-role">{{ ui[locale].role }}</p>
      </div>

      <div class="hero-body">
        <div class="hero-left">
          <p class="hero-bio">{{ ui[locale].bio }}</p>

          <div class="edu-block">
            <p class="edu-label">{{ ui[locale].eduLabel }}</p>
            <div class="edu-list">
              <div v-for="(item, i) in ui[locale].edu" :key="i" class="edu-item">
                <div class="edu-main">
                  <span class="edu-degree">{{ item.degree }}</span>
                  <span v-if="item.badge" class="edu-badge">{{ item.badge }}</span>
                </div>
                <div class="edu-sub">
                  <span class="edu-school">{{ item.school }}</span>
                  <span class="edu-period">{{ item.period }}</span>
                </div>
                <p v-if="item.detail" class="edu-detail">{{ item.detail }}</p>
              </div>
            </div>
          </div>
        </div>

        <div class="skills-block">
          <div v-for="key in ['ai', 'dev', 'tools']" :key="key" class="skill-group">
            <span class="skill-label">{{ ui[locale].skillLabels[key] }}</span>
            <div class="skill-tags">
              <span v-for="item in skills[key]" :key="item" class="tag">{{ item }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero-section {
  padding-top: 72px;
  padding-bottom: 64px;
  border-bottom: 1px solid var(--border);
}

.hero-top { margin-bottom: 40px; }

.hero-name {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(42px, 7vw, 72px);
  font-weight: 400;
  line-height: 1.05;
  letter-spacing: -0.02em;
  color: var(--text-900);
  margin-bottom: 8px;
}

.hero-role {
  font-size: 17px;
  font-weight: 300;
  color: var(--text-600);
  letter-spacing: -0.01em;
}

.hero-body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 64px;
  align-items: start;
}

.hero-left {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

.hero-bio {
  font-size: 16px;
  line-height: 1.7;
  color: var(--text-600);
  font-weight: 300;
}

.edu-block {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.edu-label {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-400);
}

.edu-list {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.edu-item {
  display: flex;
  flex-direction: column;
  gap: 3px;
  padding-left: 14px;
  border-left: 2px solid var(--border);
}

.edu-main {
  display: flex;
  align-items: center;
  gap: 8px;
  flex-wrap: wrap;
}

.edu-degree {
  font-size: 14px;
  font-weight: 500;
  color: var(--text-900);
}

.edu-badge {
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--accent);
  background: var(--accent-light);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 1px 8px;
}

.edu-detail {
  font-size: 13px;
  line-height: 1.6;
  color: var(--text-900);
  font-weight: 400;
  margin-top: 4px;
}

.edu-sub {
  display: flex;
  gap: 6px;
  align-items: center;
}

.edu-school {
  font-size: 13px;
  color: var(--text-600);
  font-weight: 300;
}

.edu-period {
  font-size: 12px;
  color: var(--text-400);
}

.skills-block {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.skill-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.skill-label {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-400);
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tag {
  display: inline-block;
  font-size: 13px;
  font-weight: 400;
  color: var(--accent);
  background: var(--accent-light);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 4px 12px;
}

@media (max-width: 640px) {
  .hero-body { grid-template-columns: 1fr; gap: 32px; }
}
</style>
