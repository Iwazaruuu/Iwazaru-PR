<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const activeSection = ref('hero')

const handleScroll = () => {
  scrolled.value = window.scrollY > 50

  const sections = ['hero', 'projects', 'skills', 'contact']
  for (const id of sections) {
    const el = document.getElementById(id)
    if (el) {
      const rect = el.getBoundingClientRect()
      if (rect.top <= 120 && rect.bottom >= 120) {
        activeSection.value = id
        break
      }
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})
onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const scrollTo = (id) => {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <nav class="nav" :class="{ scrolled }">
    <div class="nav-logo" @click="scrollTo('hero')">Портфолио</div>
    <ul class="nav-links">
      <li><a href="#projects" :class="{ active: activeSection === 'projects' }" @click.prevent="scrollTo('projects')">Проекты</a></li>
      <li><a href="#skills" :class="{ active: activeSection === 'skills' }" @click.prevent="scrollTo('skills')">Навыки</a></li>
      <li><a href="#contact" :class="{ active: activeSection === 'contact' }" @click.prevent="scrollTo('contact')">Контакты</a></li>
    </ul>
  </nav>
</template>