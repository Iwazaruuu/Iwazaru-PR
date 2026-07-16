<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const headerRef = ref(null)

const skills = [
  'SQL / MariaDB', 'REST API', 'Node.js', 'Vue.js',
  'Supabase', 'Telegram-боты (aiogram)', 'Riot API', 'Tracker.gg',
  'Интеграция сервисов', 'Анализ и поиск данных', 'Диагностика тех. проблем',
  'Медицинские инфосистемы', 'Автоматизация задач',
  'Adobe Photoshop', 'UI / Графический дизайн'
]

onMounted(() => {
  const ctx = gsap.context(() => {
    gsap.from(headerRef.value, {
      scrollTrigger: {
        trigger: sectionRef.value,
        start: 'top 85%',
        toggleActions: 'play none none none'
      },
      opacity: 0,
      y: 40,
      duration: 0.8,
      ease: 'power3.out'
    })

    gsap.fromTo('.skills-section .skill-item',
      { opacity: 0, y: 24 },
      {
        opacity: 1,
        y: 0,
        duration: 0.45,
        stagger: 0.04,
        ease: 'power3.out',
        scrollTrigger: {
          trigger: sectionRef.value,
          start: 'top 72%',
          toggleActions: 'play none none none'
        }
      }
    )
  }, sectionRef.value)

  onUnmounted(() => {
    ctx.revert()
    ScrollTrigger.getAll().forEach(t => t.kill())
  })
})
</script>

<template>
  <section id="skills" ref="sectionRef" class="section skills-section">
    <div ref="headerRef" class="section-header">
      <span class="section-label">Навыки</span>
      <h2 class="section-title">Чем я владею</h2>
      <p class="section-subtitle">
        Техническая поддержка, интеграции, разработка и дизайн — широкий спектр технологий, с которыми я работаю.
      </p>
    </div>
    <div class="skills-list">
      <span v-for="skill in skills" :key="skill" class="skill-item">{{ skill }}</span>
    </div>
  </section>
</template>