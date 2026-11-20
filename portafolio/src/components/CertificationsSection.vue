<script setup>
import { inject } from 'vue'
const locale = inject('locale')

const ui = {
  es: { label: 'Certificaciones', heading: 'Certificaciones' },
  en: { label: 'Certifications', heading: 'Certifications' },
}

const certs = [
  {
    name: { es: 'Oracle AI Vector Search Certified Professional', en: 'Oracle AI Vector Search Certified Professional' },
    issuer: 'Oracle',
    year: '2026',
    link: null,
  },
  {
    name: { es: 'Certified Associate: AI Infrastructure and Operations', en: 'Certified Associate: AI Infrastructure and Operations' },
    issuer: 'Nvidia',
    year: '2025',
    link: null,
  },
  {
    name: { es: 'AWS Fundamentals: Building Serverless Applications', en: 'AWS Fundamentals: Building Serverless Applications' },
    issuer: 'Amazon Web Services (AWS)',
    year: '2023',
    link: null,
  },
  {
    name: { es: 'Oracle Certified Cloud Infrastructure Foundations Associate', en: 'Oracle Certified Cloud Infrastructure Foundations Associate' },
    issuer: 'Oracle',
    year: '2024',
    link: null,
  },
  {
    name: { es: 'Oracle Certified AI Foundations Associate', en: 'Oracle Certified AI Foundations Associate' },
    issuer: 'Oracle',
    year: '2024',
    link: null,
  },
  {
    name: { es: 'Oracle Certified Generative AI Professional', en: 'Oracle Certified Generative AI Professional' },
    issuer: 'Oracle',
    year: '2025',
    link: null,
  },
  {
    name: { es: 'Diseñando modelos de ML con Amazon Sagemaker', en: 'Designing ML Models with Amazon Sagemaker' },
    issuer: 'Coursera - Amazon Web Services (AWS)',
    year: '2021',
    link: null,
  },
  {
    name: { es: 'Generative AI with Large Language Models', en: 'Generative AI with Large Language Models' },
    issuer: 'DeepLearning.AI',
    year: '2024',
    link: null,
  },
  {
    name: { es: 'Especialización en Machine Learning', en: 'Machine Learning Specialization' },
    issuer: 'DeepLearning.AI',
    year: '2022',
    link: null,
  },
  {
    name: { es: 'Structuring Machine Learning Projects', en: 'Structuring Machine Learning Projects' },
    issuer: 'DeepLearning.AI',
    year: '2020',
    link: null,
  },
  {
    name: { es: 'Improving Deep Neural Networks: Hyperparameter tuning, Regularization and Optimization', en: 'Improving Deep Neural Networks: Hyperparameter tuning, Regularization and Optimization' },
    issuer: 'DeepLearning.AI',
    year: '2020',
    link: null,
  },
  {
    name: { es: 'Neural Networks and Deep Learning', en: 'Neural Networks and Deep Learning' },
    issuer: 'DeepLearning.AI',
    year: '2020',
    link: null,
  },
  {
    name: { es: 'Certificate of Completion - Elements of AI', en: 'Certificate of Completion - Elements of AI' },
    issuer: 'DeepLearning.AI',
    year: '2020',
    link: null,
  },
]
</script>

<template>
  <section id="certifications" class="section certs-section">
    <div class="container">
      <p class="section-label">{{ ui[locale].label }}</p>
      <h2 class="section-heading">{{ ui[locale].heading }}</h2>

      <ul class="cert-list">
        <li v-for="(cert, i) in certs" :key="i" class="cert-item">
          <div class="cert-left">
            <a
              v-if="cert.link"
              :href="cert.link"
              target="_blank"
              rel="noopener"
              class="cert-name linked"
            >{{ cert.name[locale] }} ↗</a>
            <span v-else class="cert-name">{{ cert.name[locale] }}</span>
          </div>
          <div class="cert-right">
            <span class="cert-issuer">{{ cert.issuer }}</span>
            <span class="cert-year">{{ cert.year }}</span>
          </div>
        </li>
      </ul>
    </div>
  </section>
</template>

<style scoped>
.certs-section {
  border-bottom: 1px solid var(--border);
  padding-bottom: 80px;
}

.section-heading {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(24px, 3.5vw, 36px);
  font-weight: 400;
  color: var(--text-900);
  letter-spacing: -0.02em;
  margin-bottom: 32px;
}

.cert-list {
  display: flex;
  flex-direction: column;
  max-width: 680px;
}

.cert-item {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  gap: 16px;
  padding: 13px 0;
  border-bottom: 1px solid var(--border);
}

.cert-item:last-child {
  border-bottom: none;
}

.cert-left {
  flex: 1;
  min-width: 0;
}

.cert-name {
  font-size: 14px;
  font-weight: 400;
  color: var(--text-900);
  line-height: 1.4;
}

.cert-name.linked {
  color: var(--accent);
  transition: opacity 0.15s;
}

.cert-name.linked:hover {
  opacity: 0.65;
}

.cert-right {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-shrink: 0;
}

.cert-issuer {
  font-size: 12px;
  color: var(--text-600);
}

.cert-year {
  font-size: 12px;
  color: var(--text-400);
  min-width: 36px;
  text-align: right;
}
</style>
