<script setup>
import { onUnmounted } from 'vue'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import gsap from 'gsap'
import ParticleBackground from './components/ParticleBackground.vue'
import SiteNav from './components/SiteNav.vue'
import HeroSection from './components/HeroSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'

gsap.registerPlugin(ScrollTrigger)

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(t => t.kill())
})
</script>

<template>
  <ParticleBackground />
  <SiteNav />
  <HeroSection />
  <ProjectsSection />
  <SkillsSection />
  <ContactSection />
  <FooterSection />
</template>