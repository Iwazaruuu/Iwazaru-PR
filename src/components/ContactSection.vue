<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const headerRef = ref(null)

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

    gsap.from('.contact-section .contact-link', {
      scrollTrigger: {
        trigger: sectionRef.value,
        start: 'top 80%',
        toggleActions: 'play none none none'
      },
      opacity: 0,
      y: 30,
      duration: 0.6,
      stagger: 0.12,
      ease: 'power3.out'
    })
  }, sectionRef.value)

  onUnmounted(() => {
    ctx.revert()
  })
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(t => t.kill())
})
</script>

<template>
  <section id="contact" ref="sectionRef" class="section contact-section">
    <div ref="headerRef" class="section-header">
      <span class="section-label">Контакты</span>
      <h2 class="section-title">Давайте работать вместе</h2>
      <p class="section-subtitle">
        Открыт к новым проектам и сотрудничеству. Выберите удобный способ связи.
      </p>
    </div>
    <div class="contact-links">
      <a href="mailto:hello@example.com" class="contact-link">
        Email
      </a>
      <a href="https://t.me/username" target="_blank" rel="noopener" class="contact-link">
        Telegram
      </a>
      <a href="https://github.com/Iwazaruuu" target="_blank" rel="noopener" class="contact-link">
        GitHub
      </a>
    </div>
  </section>
</template>