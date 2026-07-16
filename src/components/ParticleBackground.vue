<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvasRef = ref(null)
let animationId = null

onMounted(() => {
  const canvas = canvasRef.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')

  let particles = []
  const particleCount = 60
  const connectionDist = 140

  const resize = () => {
    canvas.width = window.innerWidth
    canvas.height = document.body.scrollHeight
  }
  resize()
  window.addEventListener('resize', resize)

  class Particle {
    constructor() {
      this.reset()
    }
    reset() {
      this.x = Math.random() * canvas.width
      this.y = Math.random() * canvas.height
      this.size = Math.random() * 2 + 0.8
      this.speedX = (Math.random() - 0.5) * 0.4
      this.speedY = (Math.random() - 0.5) * 0.4
      this.opacity = Math.random() * 0.5 + 0.15
    }
    update() {
      this.x += this.speedX
      this.y += this.speedY
      if (this.x < 0 || this.x > canvas.width) this.speedX *= -1
      if (this.y < 0 || this.y > canvas.height) this.speedY *= -1
    }
    draw() {
      ctx.beginPath()
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(108, 92, 231, ${this.opacity})`
      ctx.fill()
    }
  }

  for (let i = 0; i < particleCount; i++) {
    particles.push(new Particle())
  }

  const animate = () => {
    ctx.clearRect(0, 0, canvas.width, canvas.height)

    for (let i = 0; i < particles.length; i++) {
      particles[i].update()
      particles[i].draw()

      for (let j = i + 1; j < particles.length; j++) {
        const dx = particles[i].x - particles[j].x
        const dy = particles[i].y - particles[j].y
        const dist = Math.sqrt(dx * dx + dy * dy)

        if (dist < connectionDist) {
          const alpha = (1 - dist / connectionDist) * 0.12
          ctx.beginPath()
          ctx.moveTo(particles[i].x, particles[i].y)
          ctx.lineTo(particles[j].x, particles[j].y)
          ctx.strokeStyle = `rgba(108, 92, 231, ${alpha})`
          ctx.lineWidth = 0.5
          ctx.stroke()
        }
      }
    }
    animationId = requestAnimationFrame(animate)
  }
  animate()

  // Update canvas height on scroll
  const handleScroll = () => {
    canvas.height = document.body.scrollHeight
  }
  window.addEventListener('scroll', handleScroll, { passive: true })

  onUnmounted(() => {
    cancelAnimationFrame(animationId)
    window.removeEventListener('resize', resize)
    window.removeEventListener('scroll', handleScroll)
  })
})
</script>

<template>
  <canvas ref="canvasRef" class="particle-bg"></canvas>
</template>

<style scoped>
.particle-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  pointer-events: none;
  z-index: 0;
}
</style>