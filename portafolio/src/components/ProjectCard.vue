<script setup>
defineProps({
  project: { type: Object, required: true },
  locale: { type: String, required: true },
})
</script>

<template>
  <article class="project-card" tabindex="0" role="button" :aria-label="project.title[locale]">
    <div class="project-image" :style="{ background: project.gradient }">
      <img v-if="project.image" :src="project.image" :alt="project.title[locale]" class="project-img" />
      <div v-else class="project-placeholder">
        <span class="placeholder-label">{{ project.title[locale] }}</span>
      </div>
    </div>

    <div class="project-content">
      <div class="project-meta">
        <span class="project-type" :style="{ background: project.tagBg, color: project.tagColor }">
          {{ project.type[locale] }}
        </span>
        <span class="project-year">{{ project.year }}</span>
      </div>

      <h3 class="project-title">{{ project.title[locale] }}</h3>
      <p class="project-desc">{{ project.shortDesc[locale] }}</p>

      <div class="project-tags">
        <span v-for="tag in project.tags.slice(0, 3)" :key="tag" class="project-tag">{{ tag }}</span>
        <span v-if="project.tags.length > 3" class="project-tag muted">+{{ project.tags.length - 3 }}</span>
      </div>

      <span class="project-cta">
        {{ locale === 'es' ? 'Ver detalle →' : 'View detail →' }}
      </span>
    </div>
  </article>
</template>

<style scoped>
.project-card {
  background: var(--white);
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-card);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  display: flex;
  flex-direction: column;
  cursor: pointer;
}

.project-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-hover);
}

.project-card:hover .project-cta {
  opacity: 1;
  transform: translateX(0);
}

.project-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
  position: relative;
  flex-shrink: 0;
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top;
}

.project-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.placeholder-label {
  font-family: 'DM Serif Display', serif;
  font-size: 20px;
  color: rgba(30, 60, 30, 0.22);
  text-align: center;
  padding: 0 24px;
  line-height: 1.3;
}

.project-content {
  padding: 22px 26px 26px;
  display: flex;
  flex-direction: column;
  flex: 1;
}

.project-meta {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 10px;
}

.project-type {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border-radius: 20px;
  padding: 3px 10px;
}

.project-year {
  font-size: 12px;
  color: var(--text-400);
}

.project-title {
  font-family: 'DM Serif Display', serif;
  font-size: 21px;
  font-weight: 400;
  color: var(--text-900);
  line-height: 1.2;
  letter-spacing: -0.01em;
  margin-bottom: 8px;
}

.project-desc {
  font-size: 13.5px;
  line-height: 1.6;
  color: var(--text-600);
  font-weight: 300;
  flex: 1;
  margin-bottom: 14px;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-bottom: 14px;
}

.project-tag {
  font-size: 11px;
  color: var(--text-400);
  background: var(--bg-2);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 2px 9px;
}

.project-tag.muted {
  opacity: 0.6;
}

.project-cta {
  font-size: 12px;
  font-weight: 500;
  color: var(--accent);
  opacity: 0.5;
  transform: translateX(-4px);
  transition: opacity 0.2s, transform 0.2s;
  display: inline-block;
}
</style>
