<script setup>
import { ref, onMounted } from 'vue'
import gsap from 'gsap'

const sectionRef = ref(null)

onMounted(() => {
  gsap.from('.hero-greeting', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    delay: 0.3,
    ease: 'power3.out'
  })
  gsap.from('.hero-title', {
    opacity: 0,
    y: 60,
    duration: 1,
    delay: 0.5,
    ease: 'power3.out'
  })
  gsap.from('.hero-subtitle', {
    opacity: 0,
    y: 40,
    duration: 0.9,
    delay: 0.8,
    ease: 'power3.out'
  })
  gsap.from('.hero-cta', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    delay: 1.1,
    ease: 'power3.out'
  })
})
</script>

<template>
  <section id="hero" ref="sectionRef" class="hero">
    <div class="hero-content">
      <p class="hero-greeting">Привет, я</p>
      <h1 class="hero-title">
        <span class="gradient-text">IWAZARU</span>
      </h1>
      <p class="hero-subtitle">
        Специалист по техподдержке и интеграциям. Работаю с медицинскими инфосистемами, SQL, REST API и автоматизацией. Разрабатываю на Node.js и Vue.js, создаю Telegram-ботов. Совмещаю технический бэкграунд с UI/графическим дизайном.
      </p>
      <div class="hero-cta">
        <a href="#projects" class="btn btn-primary">
          Смотреть проекты
          <span>↓</span>
        </a>
        <a href="#contact" class="btn btn-secondary">Связаться</a>
      </div>
    </div>
  </section>
</template>