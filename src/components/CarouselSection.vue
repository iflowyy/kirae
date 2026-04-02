<template>
  <section class="carousel-section" id="projects">
    <h2 class="carousel-heading">Познакомимся ?</h2>

    <div class="viewport" ref="viewport">
      <div class="track" ref="track" :style="{ transform: `translateX(${offset}px)` }">
        <div
          v-for="(slide, i) in slides"
          :key="i"
          class="slide"
          :class="{ active: i === current }"
        >
          <!-- If video src provided, show video; otherwise show gradient placeholder -->
          <div class="slide-visual" :class="slide.grad">
            <video
              v-if="slide.video"
              :src="slide.video"
              class="slide-video"
              muted loop playsinline
              ref="videos"
            ></video>
            <div v-else class="slide-ui">
              <div class="sui-row" v-for="r in 3" :key="r">
                <div class="sui-bar" :class="r===1?'b1':r===2?'b2':'b3'"></div>
                <div class="sui-bar"></div>
              </div>
              <div class="sui-blocks">
                <div class="sui-block" v-for="b in 6" :key="b"></div>
              </div>
            </div>
            <span class="slide-tag">{{ slide.tag }}</span>
            <div class="slide-prog">
              <div class="slide-prog-bar" :style="{ width: i === current ? progWidth + '%' : '0%' }"></div>
            </div>
          </div>
          <p class="slide-cap">{{ slide.caption }}</p>
        </div>
      </div>
    </div>

    <!-- Controls: pill dots + play button — Apple style -->
    <div class="controls">
      <div class="dots-pill">
        <button
          v-for="(_, i) in slides"
          :key="i"
          class="dot"
          :class="{ active: i === current }"
          @click="goTo(i)"
        ></button>
      </div>
      <button class="play-circle" @click="togglePlay">
        <svg v-if="playing" viewBox="0 0 18 18" fill="currentColor" width="18" height="18">
          <rect x="3" y="2" width="4" height="14" rx="1.5"/>
          <rect x="11" y="2" width="4" height="14" rx="1.5"/>
        </svg>
        <svg v-else viewBox="0 0 18 18" fill="currentColor" width="18" height="18">
          <path d="M4 2.5L14.5 9 4 15.5V2.5Z"/>
        </svg>
      </button>
    </div>
  </section>
</template>



<script setup>
import { ref, computed, onMounted, onUnmounted, nextTick } from 'vue'




const slides = [
  { tag: '', caption: 'Простота .', grad: 'g1', video: '/videos/silence.mp4' },
  { tag: '', caption: 'Легкость .', grad: 'g2', video: '/videos/cold.mp4' },
  { tag: '', caption: 'Ощущение .', grad: 'g3', video: '/videos/drift.mp4' },
  { tag: '', caption: 'Ритм .', grad: 'g4', video: '/videos/mono.mp4' },
  { tag: '', caption: 'Тишина .', grad: 'g5', video: '/videos/depth.mp4' },
]



const viewport = ref(null)
const track = ref(null)
const current = ref(0)
const playing = ref(true)
const progWidth = ref(0)
const videos = ref([])

const DURATION = 5000
let autoTimer = null
let progTimer = null

function getOffset(idx) {
  if (!track.value) return 0
  const slides = track.value.querySelectorAll('.slide')
  if (!slides[idx]) return 0
  const slideW = slides[0].offsetWidth
  const gap = 14
  const vpW = viewport.value?.offsetWidth || window.innerWidth
  return -(idx * (slideW + gap) - (vpW - slideW) / 2)
}

const offset = ref(0)

function updateOffset() { offset.value = getOffset(current.value) }

function startProg() {
  clearInterval(progTimer)
  progWidth.value = 0
  const step = 100 / (DURATION / 80)
  progTimer = setInterval(() => {
    progWidth.value = Math.min(progWidth.value + step, 100)
    if (progWidth.value >= 100) clearInterval(progTimer)
  }, 80)
}

function goTo(idx) {
  current.value = (idx + slides.length) % slides.length
  nextTick(updateOffset)
  if (playing.value) startProg()
}

function startAuto() {
  clearInterval(autoTimer)
  autoTimer = setInterval(() => goTo(current.value + 1), DURATION)
}

function stopAuto() {
  clearInterval(autoTimer)
  clearInterval(progTimer)
  progWidth.value = 0
}

function togglePlay() {
  playing.value = !playing.value
  if (playing.value) { startProg(); startAuto() }
  else stopAuto()
}

onMounted(() => {
  nextTick(() => {
    updateOffset()
    startProg()
    startAuto()
  })
// 🔥 ВОТ ЭТО ДОБАВЬ
    videos.value.forEach(v => {
      if (v) v.play()
    })
    

  
  window.addEventListener('resize', updateOffset)
})

onUnmounted(() => {
  stopAuto()
  window.removeEventListener('resize', updateOffset)
})
</script>

<style scoped>


.carousel-heading {
  font-size: clamp(28px,4vw,48px);
  font-weight: 700;
  letter-spacing: -.03em;
  color: #f5f5f7;
  text-align: center;
  margin-bottom: 140px;
}


.viewport { overflow: hidden; width: 100%; }
.track {
  display: flex; gap: 14px;
  transition: transform .65s cubic-bezier(.25,.46,.45,.94);
}

.slide {
  flex: 0 0 700px;
  border-radius: 18px; overflow: hidden;
  background: #161617;
  opacity: .38; transition: opacity .5s;
}
.slide.active { opacity: 1; }
@media (max-width: 900px) { .slide { flex: 0 0 86vw; } }

.slide-visual {
  width: 100%; aspect-ratio: 16/9;
  position: relative; overflow: hidden;
}
.slide-video { width: 100%; height: 100%; object-fit: cover; }

.g1 { background: linear-gradient(135deg,#050d1f,#0a1a3a,#0d1f4a); }
.g2 { background: linear-gradient(135deg,#030d10,#061820,#051520); }
.g3 { background: linear-gradient(135deg,#080510,#120820,#180b2a); }
.g4 { background: linear-gradient(135deg,#050a15,#0a1525,#0d1c35); }
.g5 { background: linear-gradient(135deg,#020810,#071220,#051020); }

.slide-ui {
  position: absolute; inset: 16px;
  display: flex; flex-direction: column; gap: 8px;
}
.sui-row { display: flex; gap: 6px; }
.sui-bar { height: 4px; border-radius: 2px; background: rgba(255,255,255,.08); flex: 1; }
.sui-bar.b1 { background: rgba(41,151,255,.5); flex: 2; }
.sui-bar.b2 { background: rgba(0,102,204,.4); flex:1.5; }
.sui-bar.b3 { background: rgba(100,200,255,.28); }
.sui-blocks { display: grid; grid-template-columns: repeat(6,1fr); gap: 4px; margin-top: auto; }
.sui-block { height: 20px; border-radius: 3px; background: rgba(41,151,255,.18); }
.sui-block:nth-child(odd) { background: rgba(41,151,255,.28); }
.sui-block:nth-child(3n) { background: rgba(0,200,150,.18); }

.slide-tag {
  position: absolute; bottom: 14px; left: 14px;
  font-size: 11px; color: rgba(255,255,255,.4);
  letter-spacing: .06em; text-transform: uppercase;
}
.slide-prog { position: absolute; bottom: 0; left: 0; right: 0; height: 2px; background: rgba(255,255,255,.08); }
.slide-prog-bar { height: 100%; background: rgba(255,255,255,.5); transition: width .08s linear; }

.slide-cap {
  padding: 18px 22px;
  font-size: 15px; color: #f5f5f7; line-height: 1.5;
}

/* Controls */
.controls {
  display: flex; align-items: center; justify-content: center; gap: 16px;
  margin-top: 28px; padding: 0 40px;
}

.dots-pill {
  display: flex; align-items: center; gap: 7px;
  background: rgba(255,255,255,.08);
  border-radius: 100px;
  padding: 8px 14px;
}
.dot {
  height: 6px; border-radius: 3px;
  background: rgba(255,255,255,.35);
  transition: width .35s cubic-bezier(.25,.46,.45,.94), background .3s;
  width: 6px; padding: 0;
}
.dot.active { width: 22px; background: #f5f5f7; }

.play-circle {
  width: 36px; height: 36px; border-radius: 50%;
  background: rgba(255,255,255,.1);
  display: flex; align-items: center; justify-content: center;
  color: #f5f5f7; transition: background .2s;
}
.play-circle:hover { background: rgba(255,255,255,.18); }
</style>
