<script setup>
import { inject } from 'vue'
import ProjectCard from './ProjectCard.vue'

const locale = inject('locale')
const emit = defineEmits(['open-project'])

const ui = {
  es: {
    label: 'Proyectos',
    heading: 'Trabajo Seleccionado',
    sub: 'Algunos de mis proyectos con inteligencia artificial aplicada a moda.',
    moreHeading: 'Más proyectos',
  },
  en: {
    label: 'Work',
    heading: 'Selected Projects',
    sub: 'Some of my projects with AI applied to fashion.',
    moreHeading: 'More projects',
  },
}

const projects = [
  {
    id: 1,
    title: { es: 'Agente de Recomendación de Moda por Color', en: 'Color-Aware Fashion Recommendation Agent' },
    type: { es: 'Ingeniería de IA', en: 'AI Engineering' },
    year: '2026',
    shortDesc: {
      es: 'Agente de IA conectado via MCP a una herramienta de identificación de paleta de color. Analiza entradas visuales y genera recomendaciones personalizadas de moda.',
      en: 'AI agent connected via MCP to a color palette identification tool. Analyzes visual inputs and generates personalized fashion product recommendations.',
    },
    fullDesc: {
      es: `Construí un agente de IA que se conecta via MCP (Model Context Protocol) a una herramienta de identificación de paleta de color. El agente analiza imágenes del usuario, detecta su paleta estacional y genera recomendaciones personalizadas de productos de moda.\n\nConsulta una base de datos estructurada de productos para hacer match entre los resultados de la paleta detectada y los artículos disponibles, combinando atributos de visión por computadora con IA conversacional para entregar sugerencias contextualmente relevantes y visualmente coherentes.`,
      en: `Built an AI agent that connects via MCP (Model Context Protocol) to a color palette identification tool, enabling it to analyze color inputs and generate personalized fashion product recommendations.\n\nThe agent queries a structured product database to match results based on detected palette, combining computer vision attributes with conversational AI to deliver context-aware suggestions that are visually coherent with the user's seasonal color profile.`,
    },
    tags: ['Claude API', 'MCP', 'Python', 'Computer Vision', 'AI Agents', 'Fashion'],
    media: [''],
    links: [{ label: { es: 'Ver en Upwork', en: 'View on Upwork' }, href: null }],
    gradient: 'linear-gradient(135deg, #ffddd0 0%, #f5bfa8 100%)',
    tagBg: '#ffddd0', tagColor: '#7a3520', image: null,
  },
  {
    id: 2,
    title: { es: 'Vision Transformer para Comprensión de Imágenes de Moda', en: 'Attention-Aware Vision Transformer for Fashion Image Understanding' },
    type: { es: 'Investigación ML', en: 'ML Research' },
    year: '2026',
    shortDesc: {
      es: 'Investigación de función de pérdida personalizada para reducir redundancia entre attention heads en un ViT entrenado sobre imágenes de moda. Incluye visualización de attention maps.',
      en: 'Custom loss function research to reduce redundant information sharing across attention heads in a ViT trained on fashion images. Includes attention map visualization.',
    },
    fullDesc: {
      es: `Proyecto de investigación en curso que diseña una función de pérdida personalizada para reducir la compartición de información redundante entre attention heads en un Vision Transformer (ViT) entrenado sobre imágenes de moda.\n\nEl objetivo es forzar la especialización de cada head — animando a cada uno a capturar características visuales distintas como forma, textura, silueta y regiones de color. El proyecto incluye visualización de attention maps para interpretabilidad y análisis del comportamiento de los heads a través de diferentes categorías de prendas.`,
      en: `Ongoing research project designing a custom loss function to reduce redundant information sharing across attention heads in a Vision Transformer (ViT) trained on fashion images.\n\nThe objective is to enforce head specialization — encouraging each head to capture distinct visual features such as shape, texture, silhouette, and color regions. Includes attention map visualization for interpretability and head behavior analysis across garment categories.`,
    },
    tags: ['PyTorch', 'Vision Transformers', 'Computer Vision', 'Machine Learning', 'Research', 'Fashion'],
    media: [],
    links: [{ label: { es: 'Ver paper', en: 'View paper' }, href: null }],
    gradient: 'linear-gradient(135deg, #e4dcf5 0%, #cec0f0 100%)',
    tagBg: '#e4dcf5', tagColor: '#3d2a6b', image: null,
  },
  {
    id: 3,
    title: { es: 'Agente de Investigación de Moda con Base de Conocimiento Vogue', en: 'Fashion Research Agent with Vogue Knowledge Base' },
    type: { es: 'Ingeniería de IA', en: 'AI Engineering' },
    year: '2026',
    shortDesc: {
      es: 'Agente Claude para investigación profunda de moda que combina una base de conocimiento de artículos Vogue con búsqueda web en tiempo real.',
      en: 'Claude agent for deep fashion research combining a curated Vogue article knowledge base with live internet search.',
    },
    fullDesc: {
      es: `Construí un agente Claude para investigación profunda de moda que combina dos herramientas de recuperación: una base de conocimiento curada de artículos de Vogue y búsqueda web en vivo.\n\nCuando se consulta sobre un diseñador, estética o concepto de moda, el agente decide qué fuente consultar — o ambas — sintetizando respuestas fundamentadas y ricas en contexto. Demostrado consultando el lenguaje estético y de diseño de Alexandra O'Neill, extrayendo tanto cobertura editorial como resultados web en tiempo real.`,
      en: `Built a Claude agent for deep fashion research that combines two retrieval tools: a curated knowledge base of Vogue articles and live internet search.\n\nWhen queried about a designer, aesthetic, or fashion concept, the agent decides which source to consult — or both — synthesizing grounded, context-rich responses. Demonstrated querying the aesthetic and design language of Alexandra O'Neill, pulling from editorial coverage and real-time web results.`,
    },
    tags: ['Claude API', 'RAG', 'Knowledge Base', 'Python', 'AI Agents', 'Fashion'],
    media: [],
    links: [{ label: { es: 'Ver en Upwork', en: 'View on Upwork' }, href: null }],
    gradient: 'linear-gradient(135deg, #d0e8f8 0%, #aed4f5 100%)',
    tagBg: '#d0e8f8', tagColor: '#1a4a6b', image: null,
  },
  {
    id: 4,
    title: { es: 'Optimización de Cadena de Suministro de Cápsulas', en: 'Capsule Supply Chain Optimization' },
    type: { es: 'Análisis de Datos', en: 'Data Analysis' },
    year: '2024',
    shortDesc: {
      es: 'Modelo de programación lineal para optimizar la producción y distribución de cápsulas en múltiples instalaciones. Redujo el desperdicio un 18%.',
      en: 'Linear programming model to optimize capsule production and allocation across multiple facilities. Reduced waste by 18%.',
    },
    fullDesc: {
      es: `Desarrollé un modelo de programación lineal (método simplex) para optimizar la producción y distribución de cápsulas en una cadena de suministro con múltiples instalaciones. El modelo considera restricciones de capacidad de producción, demanda mínima garantizada por zona y costos de transporte entre instalaciones.\n\nEl resultado fue una reducción del 18% en desperdicios de materia prima y una mejora significativa en la eficiencia operativa. La implementación se hizo en Python usando PuLP, con visualizaciones en matplotlib para comunicar los resultados al equipo de operaciones.`,
      en: `Developed a linear programming model (simplex method) to optimize capsule production and distribution across a multi-facility supply chain. The model accounts for production capacity constraints, guaranteed minimum demand per zone, and inter-facility transportation costs.\n\nThe result was an 18% reduction in raw material waste and a significant improvement in operational efficiency. Implemented in Python using PuLP, with matplotlib visualizations to communicate results to the operations team.`,
    },
    tags: ['Python', 'Linear Programming', 'PuLP', 'Optimization', 'Operations Research'],
    media: [],
    links: [{ label: { es: 'Ver notebook', en: 'View notebook' }, href: null }],
    gradient: 'linear-gradient(135deg, #fef4c0 0%, #fde090 100%)',
    tagBg: '#fef4c0', tagColor: '#6b4e00', image: null,
  },
  {
    id: 5,
    title: { es: 'Dashboard de Análisis de Armonía', en: 'Harmony Analysis Dashboard' },
    type: { es: 'Visualización de Datos', en: 'Data Visualization' },
    year: '2024',
    shortDesc: {
      es: 'Dashboard interactivo para comunicar resultados complejos de optimización a stakeholders no técnicos. Explora escenarios y exporta reportes.',
      en: 'Interactive dashboard to communicate complex optimization results to non-technical stakeholders. Explore scenarios and export reports.',
    },
    fullDesc: {
      es: `Dashboard interactivo construido en Python para visualizar los resultados de un análisis de optimización de armonía. El reto principal fue traducir resultados matemáticos complejos en visualizaciones comprensibles para tomadores de decisiones sin formación técnica.\n\nPermite explorar escenarios, comparar soluciones óptimas vs. actuales y exportar reportes. Construido con Plotly y Jupyter para prototipado rápido, luego refinado para presentaciones ejecutivas.`,
      en: `Interactive dashboard built in Python to visualize harmony optimization analysis results. The main challenge was translating complex mathematical outputs into understandable visualizations for non-technical decision-makers.\n\nAllows exploring scenarios, comparing optimal vs. current solutions, and exporting reports. Built with Plotly and Jupyter for rapid prototyping, then refined for executive presentations.`,
    },
    tags: ['Python', 'Plotly', 'Jupyter', 'Pandas', 'Data Viz', 'Optimization'],
    media: [],
    links: [{ label: { es: 'Ver notebook', en: 'View notebook' }, href: null }],
    gradient: 'linear-gradient(135deg, #d0f5ec 0%, #a8edda 100%)',
    tagBg: '#d0f5ec', tagColor: '#1a5a44', image: null,
  },
  {
    id: 6,
    title: { es: 'Nombre del Proyecto 6', en: 'Project Name Six' },
    type: { es: 'Diseño de Producto', en: 'Product Design' },
    year: '2023',
    shortDesc: {
      es: 'Descripción breve del proyecto. Reemplaza con tu contenido real.',
      en: 'Brief project description. Replace with your actual content.',
    },
    fullDesc: {
      es: `Descripción completa del proyecto. Reemplaza este texto con el detalle real de lo que construiste, cuál fue el reto, qué decisiones tomaste y cuáles fueron los resultados.`,
      en: `Full project description. Replace this text with the real detail of what you built, what the challenge was, what decisions you made, and what the results were.`,
    },
    tags: ['Figma', 'UX Research', 'Prototyping'],
    media: [],
    links: [{ label: { es: 'Ver proyecto', en: 'View project' }, href: null }],
    gradient: 'linear-gradient(135deg, #fce4ef 0%, #f5c0d5 100%)',
    tagBg: '#fce4ef', tagColor: '#6b1a3a', image: null,
  },
]

const moreProjects = [
  {
    id: 'm1',
    title: { es: 'Proyecto adicional A', en: 'Additional Project A' },
    type: { es: 'Análisis de Datos', en: 'Data Analysis' },
    year: '2022',
    link: null,
  },
  {
    id: 'm2',
    title: { es: 'Proyecto adicional B', en: 'Additional Project B' },
    type: { es: 'Diseño UI', en: 'UI Design' },
    year: '2022',
    link: null,
  },
  {
    id: 'm3',
    title: { es: 'Proyecto adicional C', en: 'Additional Project C' },
    type: { es: 'Investigación', en: 'Research' },
    year: '2021',
    link: null,
  },
]
</script>

<template>
  <section id="work" class="section work-section">
    <div class="container">
      <p class="section-label">{{ ui[locale].label }}</p>
      <h2 class="section-heading">{{ ui[locale].heading }}</h2>
      <p class="section-sub">{{ ui[locale].sub }}</p>

      <div class="project-grid">
        <ProjectCard
          v-for="project in projects"
          :key="project.id"
          :project="project"
          :locale="locale"
          @click="emit('open-project', project)"
        />
      </div>

      <div class="more-projects">
        <p class="more-heading">{{ ui[locale].moreHeading }}</p>
        <ul class="more-list">
          <li v-for="p in moreProjects" :key="p.id" class="more-item">
            <div class="more-left">
              <span class="more-title">{{ p.title[locale] }}</span>
              <span class="more-type">{{ p.type[locale] }}</span>
            </div>
            <div class="more-right">
              <span class="more-year">{{ p.year }}</span>
              <a v-if="p.link" :href="p.link" target="_blank" rel="noopener" class="more-link">↗</a>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<style scoped>
.work-section {
  padding-bottom: 80px;
  border-bottom: 1px solid var(--border);
}

.section-heading {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(28px, 4vw, 42px);
  font-weight: 400;
  color: var(--text-900);
  letter-spacing: -0.02em;
  margin-bottom: 8px;
}

.section-sub {
  font-size: 16px;
  font-weight: 300;
  color: var(--text-600);
  margin-bottom: 48px;
}

.project-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  margin-bottom: 56px;
}

.more-projects {
  border-top: 1px solid var(--border);
  padding-top: 36px;
}

.more-heading {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-400);
  margin-bottom: 16px;
}

.more-list { display: flex; flex-direction: column; }

.more-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 14px 0;
  border-bottom: 1px solid var(--border);
}

.more-item:last-child { border-bottom: none; }

.more-left {
  display: flex;
  align-items: baseline;
  gap: 12px;
  flex: 1;
  min-width: 0;
}

.more-title {
  font-size: 15px;
  font-weight: 400;
  color: var(--text-900);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.more-type {
  font-size: 12px;
  color: var(--text-400);
  white-space: nowrap;
}

.more-right {
  display: flex;
  align-items: center;
  gap: 12px;
  flex-shrink: 0;
}

.more-year { font-size: 12px; color: var(--text-400); }

.more-link {
  font-size: 14px;
  color: var(--accent);
  transition: opacity 0.15s;
}

.more-link:hover { opacity: 0.6; }

@media (max-width: 680px) {
  .project-grid { grid-template-columns: 1fr; }
}
</style>
