<template>
  <footer id="contact">
    <div class="ft-breadcrumb">
      <span>kirae</span><span class="sep"> › </span><span>Портфолио</span>
    </div>
    <div class="ft-grid">
      <div class="ft-col" v-for="col in cols" :key="col.title">
        <h4>{{ col.title }}</h4>
        <a v-for="link in col.links" :key="link" href="#">{{ link }}</a>
      </div>
    </div>
    <div class="ft-bottom">
      <p>Copyright &copy; 2025 kirae . Все права защищены .</p>
      <div class="ft-links">
        <a href="#">Политика конфиденциальности</a>
        <a href="#">Контакт</a>
      </div>
    </div>
  </footer>
</template>

<script setup>
const cols = [
  { title: 'Проекты', links: ['Монтаж','Moodboard','Анимация','Цвет'] },
  { title: 'Контакт', links: ['Telegram','Instagram','Email'] },
  { title: 'Подход', links: ['О процессе','Брифование','Сроки'] },
  { title: 'Прочее', links: ['GitHub','Behance','Vimeo'] },
]
</script>

<style scoped>
footer { border-top: 1px solid rgba(255,255,255,.1); }
.ft-breadcrumb {
  max-width: 980px; margin: 0 auto;
  padding: 14px 40px;
  font-size: 12px; color: #6e6e73;
  border-bottom: 1px solid rgba(255,255,255,.1);
  display: flex; gap: 6px;
}
.sep { opacity: .4; }
.ft-grid {
  max-width: 980px; margin: 0 auto;
  padding: 28px 40px 36px;
  display: grid; grid-template-columns: repeat(4,1fr); gap: 24px;
}
.ft-col h4 { font-size: 12px; font-weight: 600; color: #6e6e73; margin-bottom: 10px; }
.ft-col a { display: block; font-size: 12px; color: #6e6e73; margin-bottom: 8px; transition: color .2s; }
.ft-col a:hover { color: #f5f5f7; }
.ft-bottom {
  max-width: 980px; margin: 0 auto;
  padding: 16px 40px;
  border-top: 1px solid rgba(255,255,255,.1);
  display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 12px;
}
.ft-bottom p { font-size: 12px; color: #6e6e73; }
.ft-links { display: flex; gap: 20px; }
.ft-links a { font-size: 12px; color: #6e6e73; transition: color .2s; }
.ft-links a:hover { color: #f5f5f7; }
@media (max-width: 768px) {
  .ft-grid { grid-template-columns: 1fr 1fr; padding: 24px 20px; }
  .ft-breadcrumb, .ft-bottom { padding: 14px 20px; }
}
</style>
