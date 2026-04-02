<template>
  <nav :class="['nav', { scrolled }]">
    <div class="nav-inner">
      <a href="#" class="nav-logo">kirae</a>
      <div class="nav-right">
        <a href="#projects" class="nav-link">Посмотреть проекты</a>
        <a href="#contact" class="nav-cta">Контакт</a>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
const scrolled = ref(false)
const onScroll = () => { scrolled.value = window.scrollY > 8 }
onMounted(() => window.addEventListener('scroll', onScroll))
onUnmounted(() => window.removeEventListener('scroll', onScroll))
</script>

<style scoped>
.nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  height: 44px;
  display: flex; align-items: center;
  padding: 0 22px;
  transition: background .4s ease, border-bottom .4s ease;
}
.nav.scrolled {
  background: rgba(8, 8, 8, 0.9);
  backdrop-filter: blur(16px) saturate(120%);
  -webkit-backdrop-filter: blur(16px) saturate(120%);
  border-bottom: 1px solid rgba(255,255,255,0.06);
}
.nav-inner {
  display: flex; align-items: center; justify-content: space-between;
  width: 100%; max-width: 980px; margin: 0 auto;
}
.nav-logo { font-size: 21px; font-weight: 600; letter-spacing: -0.02em; color: #f5f5f7; }
.nav-right { display: flex; align-items: center; gap: 24px; }
.nav-link { font-size: 13px; color: #6e6e73; transition: color .2s; }
.nav-link:hover { color: #f5f5f7; }
.nav-cta {
  font-size: 13px; font-weight: 500; color: #fff;
  background: #0066cc; padding: 6px 16px; border-radius: 100px;
  transition: background .2s;
}
.nav-cta:hover { background: #0077ed; }
@media (max-width: 600px) { .nav-link { display: none; } }
</style>