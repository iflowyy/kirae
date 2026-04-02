<template>
  <section class="features" id="about">
    <div class="feat-top">
      <div class="feat-info">
        
        <h2 class="feat-title">Кадр , который<br>чувствуется .</h2>
        <p class="feat-desc">
          Каждый проект - это про <strong>ощущение ,</strong> а не про количество эффектов .
          Работаю с ритмом , цветом и <strong>тишиной</strong> между кадрами .
        </p>
      </div>
    
    </div>

    <div class="feat-scroll" ref="scrollArea">
      <div class="feat-track" ref="featTrack" :style="{ transform: `translateX(${featOffset}px)` }">
        <div class="feat-card" v-for="card in cards" :key="card.title">
          <div class="feat-visual" :class="card.grad">
            <div class="fv-ui">
              <div class="fv-row fa"></div>
              <div class="fv-row fb"></div>
              <div class="fv-row fa"></div>
              <div class="fv-dots">
                <div class="fv-dot" v-for="n in 5" :key="n"></div>
              </div>
            </div>
          </div>
          <div class="feat-body">
            <p class="feat-name"><strong>{{ card.title }}.</strong> <span>{{ card.sub }}</span></p>
            <p class="feat-desc2">{{ card.desc }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted, nextTick } from 'vue'

const cards = [
  { title: 'Монтаж видео', sub: 'Нарратив через ритм.', desc: 'Работаю с темпом кадра и звуком. Каждая склейка - это решение, а не случайность.', grad: 'fv1' },
  { title: 'Цвет', sub: 'Настроение кадра.', desc: 'Колористика - это не фильтр, это характер. Подбираю палитру под задачу.', grad: 'fv2' },
  { title: 'Moodboard', sub: 'Визуальная идея до съёмки.', desc: 'Собираю референсы и концепцию до начала работы. Так меньше правок и больше точности.', grad: 'fv3' },
  { title: 'Анимация', sub: 'Движение с умыслом.', desc: 'Плавные переходы и графика, которая не кричит, а дополняет.', grad: 'fv4' },
]

const scrollArea = ref(null)
const featTrack = ref(null)
const idx = ref(0)
const featOffset = ref(0)

const cardW = () => {
  const card = featTrack.value?.querySelector('.feat-card')
  return card ? card.offsetWidth + 14 : 334
}

const visibleCount = () => {
  const w = scrollArea.value?.offsetWidth || window.innerWidth
  return Math.floor(w / cardW())
}

const atEnd = computed(() => idx.value >= cards.length - visibleCount())

function scroll(dir) {
  idx.value = Math.max(0, Math.min(cards.length - visibleCount(), idx.value + dir))
  featOffset.value = -idx.value * cardW()
}

const onResize = () => { idx.value = 0; featOffset.value = 0 }
onMounted(() => window.addEventListener('resize', onResize))
onUnmounted(() => window.removeEventListener('resize', onResize))
</script>







<style scoped>
.features { padding: 140px 0; }

.feat-top {
  display: flex;
  justify-content: center;
  padding: 0 40px;
  margin-bottom: 150px; /* было 32 */
}





.feat-info { flex: 1; max-width: 560px; }
.feat-label { font-size: 13px; font-weight: 600; letter-spacing: .05em; text-transform: uppercase; color: #2997ff; margin-bottom: 10px; }
.feat-title { font-size: clamp(28px,4vw,44px); font-weight: 700; letter-spacing: -.03em; color: #f5f5f7; margin-bottom: 14px; line-height: 1.1; }
.feat-desc  { font-size: 17px; font-weight: 300; color: #6e6e73; line-height: 1.7; }
.feat-desc strong { color: #f5f5f7; font-weight: 500; }

.feat-btns { display: flex; gap: 8px; padding-top: 6px; flex-shrink: 0; }
.arr-btn {
  width: 36px; height: 36px; border-radius: 50%;
  border: 1px solid rgba(255,255,255,.15);
  color: #f5f5f7; font-size: 18px;
  display: flex; align-items: center; justify-content: center;
  transition: border-color .2s;
}
.arr-btn:hover:not(:disabled) { border-color: #f5f5f7; }
.arr-btn:disabled { opacity: .3; pointer-events: none; }

.feat-scroll { overflow: hidden; }



.feat-track {
  display: flex;
  gap: 14px;
  padding: 0 40px 4px;
  justify-content: center; /* ВОТ ЭТО ДОБАВЬ */
  transition: transform .5s cubic-bezier(.25,.46,.45,.94);
}


.feat-info {
  text-align: center;
  max-width: 520px; /* чуть уже */
}





.feat-card {
  flex: 0 0 320px;
  background: #161617; border-radius: 16px; overflow: hidden;
}
.feat-visual { width: 100%; aspect-ratio: 4/3; position: relative; }
.fv1 { background: linear-gradient(135deg,#050d1f,#0d2040); }
.fv2 { background: linear-gradient(135deg,#04080f,#0a1428); }
.fv3 { background: linear-gradient(135deg,#080510,#120b20); }
.fv4 { background: linear-gradient(135deg,#040810,#081225); }

.fv-ui { position: absolute; inset: 12px; display: flex; flex-direction: column; gap: 6px; }
.fv-row { height: 3px; border-radius: 2px; background: rgba(255,255,255,.08); }
.fv-row.fa { background: rgba(41,151,255,.45); width: 70%; }
.fv-row.fb { background: rgba(41,151,255,.28); width: 50%; }
.fv-dots { display: grid; grid-template-columns: repeat(5,1fr); gap: 4px; margin-top: auto; }
.fv-dot  { height: 16px; border-radius: 3px; background: rgba(41,151,255,.15); }
.fv-dot:nth-child(2n) { background: rgba(0,200,150,.18); }
.fv-dot:nth-child(3n) { background: rgba(41,151,255,.28); }

.feat-body { padding: 16px 18px 20px; }
.feat-name { font-size: 14px; color: #a1a1a6; margin-bottom: 6px; line-height: 1.5; }
.feat-name strong { color: #f5f5f7; }
.feat-desc2 { font-size: 13px; color: #6e6e73; line-height: 1.6; }

@media (max-width: 768px) {
  .feat-top { flex-direction: column; padding: 0 20px; }
  .feat-track { padding: 0 20px 4px; }
}
</style>
