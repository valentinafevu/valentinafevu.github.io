<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  project: { type: Object, required: true },
  locale: { type: String, required: true },
})
const emit = defineEmits(['close'])

const activeMediaIndex = ref(0)

const hasMedia = computed(() => props.project.media && props.project.media.length > 0)

const paragraphs = computed(() =>
  (props.project.fullDesc[props.locale] || '').split('\n\n').filter(Boolean)
)

function onBackdropClick(e) {
  if (e.target === e.currentTarget) emit('close')
}

function onKeydown(e) {
  if (e.key === 'Escape') emit('close')
}

const ui = {
  es: { close: 'Cerrar', links: 'Links', tags: 'Tecnologías', noMedia: 'Aquí irán las imágenes y videos del proyecto.' },
  en: { close: 'Close', links: 'Links', tags: 'Tech & Tools', noMedia: 'Images and videos of the project will go here.' },
}
</script>

<template>
  <Teleport to="body">
    <div
      class="modal-backdrop"
      @click="onBackdropClick"
      @keydown="onKeydown"
      tabindex="-1"
    >
      <div class="modal" role="dialog" :aria-label="project.title[locale]">
        <!-- Header -->
        <div class="modal-header">
          <div class="modal-header-meta">
            <span
              class="modal-type"
              :style="{ background: project.tagBg, color: project.tagColor }"
            >{{ project.type[locale] }}</span>
            <span class="modal-year">{{ project.year }}</span>
          </div>
          <button class="modal-close" @click="emit('close')" :aria-label="ui[locale].close">
            <svg width="18" height="18" viewBox="0 0 18 18" fill="none">
              <path d="M1 1l16 16M17 1L1 17" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"/>
            </svg>
          </button>
        </div>

        <div class="modal-body">
          <!-- Title -->
          <h2 class="modal-title">{{ project.title[locale] }}</h2>

          <!-- Media gallery -->
          <div class="modal-media">
            <div v-if="hasMedia" class="media-main">
              <template v-if="project.media[activeMediaIndex].type === 'image'">
                <img
                  :src="project.media[activeMediaIndex].src"
                  :alt="project.title[locale]"
                  class="media-image"
                />
              </template>
              <template v-else-if="project.media[activeMediaIndex].type === 'youtube'">
                <iframe
                  class="media-video"
                  :src="`https://www.youtube.com/embed/${project.media[activeMediaIndex].id}`"
                  frameborder="0"
                  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                  allowfullscreen
                />
              </template>
              <template v-else-if="project.media[activeMediaIndex].type === 'video'">
                <video class="media-video" controls :src="project.media[activeMediaIndex].src" />
              </template>
            </div>

            <div v-else class="media-placeholder" :style="{ background: project.gradient }">
              <p class="media-placeholder-text">{{ ui[locale].noMedia }}</p>
            </div>

            <!-- Thumbnails -->
            <div v-if="hasMedia && project.media.length > 1" class="media-thumbs">
              <button
                v-for="(item, i) in project.media"
                :key="i"
                :class="['thumb-btn', { active: activeMediaIndex === i }]"
                @click="activeMediaIndex = i"
              >
                <img
                  v-if="item.type === 'image'"
                  :src="item.src"
                  class="thumb-img"
                  :alt="`Media ${i + 1}`"
                />
                <div v-else class="thumb-video-icon">▶</div>
              </button>
            </div>
          </div>

          <!-- Content grid -->
          <div class="modal-content-grid">
            <!-- Description -->
            <div class="modal-desc">
              <p v-for="(para, i) in paragraphs" :key="i" class="modal-para">{{ para }}</p>
            </div>

            <!-- Sidebar: tags + links -->
            <aside class="modal-sidebar">
              <div class="sidebar-block">
                <p class="sidebar-label">{{ ui[locale].tags }}</p>
                <div class="sidebar-tags">
                  <span v-for="tag in project.tags" :key="tag" class="sidebar-tag">{{ tag }}</span>
                </div>
              </div>

              <div v-if="project.links && project.links.length" class="sidebar-block">
                <p class="sidebar-label">{{ ui[locale].links }}</p>
                <div class="sidebar-links">
                  <template v-for="link in project.links" :key="link.label[locale]">
                    <a
                      v-if="link.href"
                      :href="link.href"
                      target="_blank"
                      rel="noopener"
                      class="sidebar-link"
                    >{{ link.label[locale] }} ↗</a>
                    <span v-else class="sidebar-link disabled">{{ link.label[locale] }}</span>
                  </template>
                </div>
              </div>
            </aside>
          </div>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 200;
  background: rgba(18, 30, 18, 0.45);
  backdrop-filter: blur(6px);
  display: flex;
  align-items: flex-end;
  justify-content: center;
  padding: 0;
  animation: backdrop-in 0.25s ease;
}

@keyframes backdrop-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}

.modal {
  background: var(--white);
  width: 100%;
  max-width: 820px;
  max-height: 92vh;
  border-radius: var(--radius-lg) var(--radius-lg) 0 0;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  animation: modal-up 0.3s cubic-bezier(0.22, 1, 0.36, 1);
}

@keyframes modal-up {
  from { transform: translateY(40px); opacity: 0; }
  to   { transform: translateY(0);    opacity: 1; }
}

/* on wider screens, center the modal with rounded corners all around */
@media (min-width: 860px) {
  .modal-backdrop {
    align-items: center;
    padding: 24px;
  }
  .modal {
    border-radius: var(--radius-lg);
    max-height: 88vh;
    animation: modal-in 0.3s cubic-bezier(0.22, 1, 0.36, 1);
  }
}

@keyframes modal-in {
  from { transform: scale(0.96) translateY(12px); opacity: 0; }
  to   { transform: scale(1)    translateY(0);    opacity: 1; }
}

/* ── Header ── */
.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 28px 0;
  flex-shrink: 0;
}

.modal-header-meta {
  display: flex;
  align-items: center;
  gap: 10px;
}

.modal-type {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border-radius: 20px;
  padding: 3px 10px;
}

.modal-year {
  font-size: 12px;
  color: var(--text-400);
}

.modal-close {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 34px;
  height: 34px;
  border-radius: 50%;
  background: var(--bg-2);
  border: 1px solid var(--border);
  color: var(--text-600);
  cursor: pointer;
  transition: background 0.15s, color 0.15s;
  flex-shrink: 0;
}

.modal-close:hover {
  background: var(--border);
  color: var(--text-900);
}

/* ── Body ── */
.modal-body {
  padding: 20px 28px 36px;
  overflow-y: auto;
}

.modal-title {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(26px, 4vw, 38px);
  font-weight: 400;
  letter-spacing: -0.02em;
  color: var(--text-900);
  margin-bottom: 24px;
  line-height: 1.1;
}

/* ── Media ── */
.modal-media {
  margin-bottom: 32px;
}

.media-main {
  border-radius: var(--radius-md);
  overflow: hidden;
  background: var(--bg-2);
}

.media-image {
  width: 100%;
  height: auto;
  max-height: 420px;
  object-fit: cover;
  display: block;
}

.media-video {
  width: 100%;
  aspect-ratio: 16 / 9;
  display: block;
  border: none;
}

.media-placeholder {
  width: 100%;
  height: 260px;
  border-radius: var(--radius-md);
  display: flex;
  align-items: center;
  justify-content: center;
}

.media-placeholder-text {
  font-size: 13px;
  color: rgba(30, 60, 30, 0.3);
  font-style: italic;
}

.media-thumbs {
  display: flex;
  gap: 8px;
  margin-top: 10px;
  overflow-x: auto;
  padding-bottom: 2px;
}

.thumb-btn {
  width: 64px;
  height: 48px;
  border-radius: 8px;
  overflow: hidden;
  border: 2px solid transparent;
  cursor: pointer;
  background: var(--bg-2);
  padding: 0;
  flex-shrink: 0;
  transition: border-color 0.15s;
}

.thumb-btn.active {
  border-color: var(--accent);
}

.thumb-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.thumb-video-icon {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  color: var(--text-400);
}

/* ── Content grid ── */
.modal-content-grid {
  display: grid;
  grid-template-columns: 1fr 220px;
  gap: 40px;
  align-items: start;
}

.modal-desc {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.modal-para {
  font-size: 15px;
  line-height: 1.7;
  color: var(--text-600);
  font-weight: 300;
}

/* ── Sidebar ── */
.modal-sidebar {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.sidebar-block {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.sidebar-label {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-400);
}

.sidebar-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

.sidebar-tag {
  font-size: 12px;
  color: var(--accent);
  background: var(--accent-light);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 3px 10px;
}

.sidebar-links {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.sidebar-link {
  font-size: 13px;
  font-weight: 500;
  color: var(--accent);
  transition: opacity 0.15s;
  display: inline-block;
}

.sidebar-link:hover {
  opacity: 0.65;
}

.sidebar-link.disabled {
  color: var(--text-400);
  cursor: default;
  font-style: italic;
}

@media (max-width: 600px) {
  .modal-content-grid {
    grid-template-columns: 1fr;
    gap: 24px;
  }
  .modal-body {
    padding: 16px 20px 32px;
  }
  .modal-header {
    padding: 16px 20px 0;
  }
}
</style>
