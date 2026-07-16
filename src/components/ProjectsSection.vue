<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const headerRef = ref(null)
const lightboxImage = ref(null)
const showLightbox = ref(false)

const projects = [
  {
    id: 'fixlab',
    title: 'FixLab',
    desc: 'Брендинг, SMM-дизайн и оформление доставки для сервиса по ремонту техники.',
    dir: '/portfolio/Портфолио/FixLab',
    images: [
      'fixlab_ru_final.png', 'fixlab_LV_final.png', 'fixlab_ru.png',
      'fixlab_ligo_ru.png', 'fixlab_ligo_lv.png', 'fixlab_temperature_RU (1).png',
      'fixlab_temperature_LV (1).png', 'fixlab_delivery_LV (1).png',
      'fixlab_delivery_LV.png', 'fixlab_delivery (2).png', 'fixlab_delivery (3).png',
      'fixlab_1.png', 'flag_fixlab.png', 'fixlab_temperature.png',
      'Facebook post.jpg', 'Facebook post (1).jpg', 'FACEBOOK POST PC.jpg',
      'FACEBOOK POST PC (1).jpg', 'Facebook top.jpg', 'Facebook top (1).jpg',
      'story pc.jpg', 'STORY TEL.jpg'
    ]
  },
  {
    id: 'godjigame',
    title: 'Godji Game',
    desc: 'Полный визуал для стримера: VK-баннеры, плашки, анонсы турниров и holiday-кампании.',
    dir: '/portfolio/Портфолио/GodjiGame(часть работ недоступна)',
    images: [
      'VK_BANNER.png', 'VK_BANNER_V2.png', 'VK_BANNER_V3.png', 'VK_BANNER_V4.png',
      'VK_BANNER_V5.png', 'VK_BANNER_V6.png', 'VK_BANNER_V7.png', 'banner_gdj.png',
      'GodjiZastavka2024.png', 'Pre_zastavka.png', 'godjiad.png', 'godjiad_vert.png',
      'godjhalloween2.png', 'godjiheloween.png', 'godji_ny.png', 'godjibirth.png',
      'GODJIFEMALEDAY.png', 'godjiPCSStandart.png', 'godjiPCSVip.png',
      'godjiwidjet_final_final_tochno.png', 'godjicoffee.png', 'godjicoin.png',
      'ADgodji.png', '2GIS.png', 'baldursgate3.png', 'fc25.png', 'games.png',
      'cashback_godji.png', 'meme_godji.png', 'non-alco.png', 'non-alco (2).png',
      'non-food.png', 'opencase.png', 'pcs.png', 'PRICE.png', 'pricelist.png',
      'pricelist (2).png', 'pricelist (3).png', 'ps5games.png', 'ref.png',
      'sale.png', 'tavern.png', 'tournamentAd.png', 'tap_godji.png', 'news.png',
      'map_review.png', 'image_2024-10-13_03-03-40.png'
    ]
  },
  {
    id: 'godji-new',
    title: 'Godji — Новый стиль',
    desc: 'Обновление визуального стиля: логотип, плашки, турнирные афиши и оформление сообщества.',
    dir: '/portfolio/Портфолио/godjiNewStylePNGS',
    images: [
      'gg_logo.png', 'logogodji.png', 'GodjiZastavka2024_v2.png',
      'godjibirthday.png', 'giveaway.png', 'rules.png', 'VK_LOGO.png',
      'promo/godjiplus.png', 'promo/map_review.png',
      'tournaments/cs2_1x1.png', 'tournaments/cs2_2x2.png',
      'posts/cs2 tournament', 'posts/top 5',
      'VK_PLATES/VK_BANNER.png', 'VK_PLATES/VK_BANNER_V2.png',
      'VK_PLATES/VK_BANNER_V3.png', 'VK_PLATES/VK_BANNER_V4.png',
      'VK_PLATES/VK_BANNER_V5.png', 'VK_PLATES/VK_BANNER_V6.png',
      'VK_PLATES/VK_BANNER_V7.png', 'VK_PLATES/games.png', 'VK_PLATES/godjicoin.png',
      'VK_PLATES/news.png', 'VK_PLATES/pcs.png', 'VK_PLATES/PRICE.png',
      'VK_PLATES/ref.png', 'VK_PLATES/sale.png', 'VK_PLATES/tavern.png',
      'морской бой/seabattle.png', 'морской бой/seabattle_v2.png',
      'Сертифкаты/1000.png'
    ]
  },
  {
    id: 'ttv',
    title: 'Twitch-оформление',
    desc: 'Баннеры, панели и офлайн-заставка для Twitch-канала.',
    dir: '/portfolio/Портфолио/ttv',
    images: [
      'banner.png', 'logo_twitch.png', 'offline.png', 'socials.png',
      'PANELS/DISCORD.png', 'PANELS/DONATE.png', 'PANELS/INFO.png',
      'PANELS/SETUP.png', 'PANELS/TG.png', 'PANELS/YOUTUBE.png'
    ]
  },
  {
    id: 'other',
    title: 'Отдельные работы',
    desc: 'YouTube-баннеры, превью, донат-аппарат и другие графические работы.',
    dir: '/portfolio/Портфолио',
    images: [
      'banner_iwa.png', 'banner_iwa_youtube.png', 'banner_iwa_youtubex2.png',
      'banneroverdice.png', 'overdiceshark_ny.png', 'iwazaru_y2k.png',
      'youtube_banner.png', 'YOUTUBE.png', 'VIDEOPLAYER_BANNER.png',
      'try_youtube_1.png', 'try_youtube_2.png', 'bebraApex.png',
      '5am.png', 'AD.png', 'ashe.png', 'azoty.png', 'btw.png',
      'DONATE.png', 'donation_banner.png', 'icantstopme.png', 'IWAAA.png',
      'psylocke.png', 'SETUP.png', 'sharky__.png', 'smth.png',
      'so_dangerous.png', 'TELEGRAM.png', 'telegram_banner.png',
      'template_banner.png', 'theyarevoid.png', 'urpretty.png', 'V.png',
      'WATCHMEGO.png', 'Zapishi.png', 'Монтажная область 1.png'
    ]
  }
]

const openLightbox = (src) => {
  lightboxImage.value = src
  showLightbox.value = true
  document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
  showLightbox.value = false
  lightboxImage.value = null
  document.body.style.overflow = ''
}

const getSrc = (dir, img) => `${dir}/${img}`

onMounted(() => {
  const ctx = gsap.context(() => {
    // Main section header
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

    // Each project group header
    document.querySelectorAll('.project-group').forEach((group) => {
      const groupHeader = group.querySelector('.project-group-header')
      if (groupHeader) {
        gsap.from(groupHeader, {
          scrollTrigger: {
            trigger: group,
            start: 'top 78%',
            toggleActions: 'play none none none'
          },
          opacity: 0,
          y: 30,
          duration: 0.7,
          ease: 'power3.out'
        })
      }
    })

    // Intersection Observer for masonry items (no GSAP — pure CSS transition)
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed')
          observer.unobserve(entry.target)
        }
      })
    }, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' })

    document.querySelectorAll('.masonry-item').forEach((item) => {
      observer.observe(item)
    })
  }, sectionRef.value)

  onUnmounted(() => {
    ctx.revert()
    ScrollTrigger.getAll().forEach(t => t.kill())
  })
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(t => t.kill())
})
</script>

<template>
  <section id="projects" ref="sectionRef" class="section section-projects">
    <div ref="headerRef" class="section-header">
      <span class="section-label">Портфолио</span>
      <h2 class="section-title">Мои проекты</h2>
      <p class="section-subtitle">
        Избранные работы по брендингу, SMM-дизайну и оформлению для стримеров.
      </p>
    </div>

    <div v-for="project in projects" :key="project.id" class="project-group">
      <div class="project-group-header">
        <h3 class="project-group-title">{{ project.title }}</h3>
        <p class="project-group-desc">{{ project.desc }}</p>
      </div>
      <div class="masonry" ref="masonryRef">
        <div
          v-for="(img, idx) in project.images"
          :key="idx"
          class="masonry-item"
          @click="openLightbox(getSrc(project.dir, img))"
        >
          <img
            :src="getSrc(project.dir, img)"
            :alt="`${project.title} - ${img}`"
            loading="lazy"
          />
        </div>
      </div>
    </div>

    <!-- Lightbox -->
    <Teleport to="body">
      <div v-if="showLightbox" class="lightbox" @click.self="closeLightbox">
        <button class="lightbox-close" @click="closeLightbox">&times;</button>
        <div class="lightbox-wrapper">
          <img :src="lightboxImage" class="lightbox-image" />
          <div class="watermark">iwazaru</div>
        </div>
      </div>
    </Teleport>
  </section>
</template>