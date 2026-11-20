<script setup>
import { ref, provide } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import WorkSection from './components/WorkSection.vue'
import CertificationsSection from './components/CertificationsSection.vue'
import FooterSection from './components/FooterSection.vue'
import ProjectModal from './components/ProjectModal.vue'

const locale = ref('es')
const selectedProject = ref(null)

provide('locale', locale)
provide('selectedProject', selectedProject)

function openProject(project) {
  selectedProject.value = project
  document.body.style.overflow = 'hidden'
}

function closeProject() {
  selectedProject.value = null
  document.body.style.overflow = ''
}
</script>

<template>
  <NavBar :locale="locale" @toggle-locale="locale = locale === 'es' ? 'en' : 'es'" />
  <main>
    <HeroSection />
    <WorkSection @open-project="openProject" />
    <CertificationsSection />
    <FooterSection />
  </main>
  <ProjectModal
    v-if="selectedProject"
    :project="selectedProject"
    :locale="locale"
    @close="closeProject"
  />
</template>

<style scoped>
main { min-height: 100vh; }
</style>
