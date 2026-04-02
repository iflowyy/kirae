<template>
  <section class="faq-section" id="faq">
    <h2 class="faq-title">Ответы на ваши вопросы :</h2>
    <div class="faq-list">
      <div class="faq-item" v-for="(item, i) in faqs" :key="i" :class="{ open: openIdx === i }">
        <button class="faq-q" @click="toggle(i)">
          {{ item.q }}
          <span class="chevron">›</span>
        </button>
        <div class="faq-a" :style="openIdx === i ? { maxHeight: '200px' } : { maxHeight: '0' }">
          <div class="faq-a-inner">{{ item.a }}</div>
        </div>
      </div>
    </div>
    <div class="footnotes">
      
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'
const openIdx = ref(null)
function toggle(i) { openIdx.value = openIdx.value === i ? null : i }
const faqs = [
  { q: 'Как начать работу ?', a: 'Напишите мне - коротко опишите проект , задачу и примерные сроки . Я отвечу в течение суток .' },
  { q: 'Какие форматы финального файла ?', a: 'MP4 (H.264 или H.265) для видео , PDF или PNG для визуальных материалов . Другие форматы - по запросу .' },
  { q: 'Беру ли я проекты с нуля без съёмки ?', a: 'Да . Могу работать с вашими исходниками или помочь с концепцией и техническим заданием .' },
  { q: 'Сколько стоит ?', a: 'Зависит от объёма и сроков . Обсуждаем индивидуально после брифа . Фиксированного прайса нет .' },
  { q: 'Работаете ли вы удалённо ?', a: 'Полностью удалённо . Все правки, файлы и общение - онлайн .' },
  { q: 'Сколько итераций правок включено ?', a: 'Как правило , 2 раунда правок входят в стоимость . Дополнительные - по договорённости .' },
]
</script>

<style scoped>
.faq-section { max-width: 860px; margin: 0 auto; padding: 80px 40px 60px; }
.faq-title {
  font-size: clamp(32px,4.5vw,52px); font-weight: 700;
  letter-spacing: -.03em; color: #f5f5f7; margin-bottom: 44px;
}
.faq-list { border-top: 1px solid rgba(255,255,255,.1); }
.faq-item { border-bottom: 1px solid rgba(255,255,255,.1); }
.faq-q {
  width: 100%; display: flex; justify-content: space-between; align-items: center;
  padding: 18px 0; font-size: 17px; color: #f5f5f7; text-align: left; gap: 16px;
}
.chevron {
  flex-shrink: 0; font-size: 22px; color: #6e6e73;
  transition: transform .3s; display: inline-block;
}
.faq-item.open .chevron { transform: rotate(90deg); }
.faq-a {
  max-height: 0; overflow: hidden;
  transition: max-height .4s cubic-bezier(.25,.46,.45,.94);
}
.faq-a-inner { padding: 0 0 20px; font-size: 15px; color: #6e6e73; line-height: 1.7; max-width: 660px; }

.footnotes { margin-top: 48px; padding-top: 28px; border-top: 1px solid rgba(255,255,255,.1); }
.footnotes ol { list-style: decimal; padding-left: 18px; }
.footnotes li { font-size: 11px; color: #424245; line-height: 1.8; margin-bottom: 3px; }

@media (max-width: 600px) { .faq-section { padding: 60px 20px 40px; } }
</style>
