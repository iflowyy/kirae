<template>
  <section class="hero">
    <div class="hero-text">
      <h1 class="hero-title">Ритм . Тишина .<br>Визуал .</h1>
      <p class="hero-desc">Визуальные проекты для тех,<br>кто ценит<strong> ощущение .</strong></p>
      <div class="hero-btns">
        <a href="#projects" class="btn-primary">Смотреть проекты</a>
        <a href="#about" class="btn-ghost">Обо мне ›</a>
      </div>
    </div>
  </section>
</template>

<style scoped>


.hero {
  height: 70vh; /* фиксированная высота блока */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center; /* по центру блока */
  padding: 0 24px; /* убираем верхний паддинг */
  text-align: center;
}


.hero-mockup {
  width: 100%; max-width: 680px; margin-bottom: 52px;
}
.mock-grid {
  display: grid; grid-template-columns: 1fr 1.5fr; gap: 10px;
  background: linear-gradient(140deg, #071428 0%, #0a1a38 40%, #0c1f48 70%, #060e1a 100%);
  border-radius: 18px; padding: 18px;
  box-shadow: 0 40px 80px rgba(0,0,0,.7), 0 0 0 1px rgba(255,255,255,.06);
  aspect-ratio: 16/9;
}
.mock-panel {
  background: rgba(255,255,255,.04);
  border: 1px solid rgba(255,255,255,.06);
  border-radius: 8px; padding: 12px;
  display: flex; flex-direction: column; gap: 7px; overflow: hidden;
}
.m-row {
  height: 5px; border-radius: 3px;
  background: rgba(255,255,255,.08);
}
.m-row.accent  { background: rgba(41,151,255,.45); width: 80%; }
.m-row.accent2 { background: rgba(0,102,204,.3); width: 55%; }
.m-row.sm      { width: 40%; }
.m-blocks { display: grid; grid-template-columns: repeat(4,1fr); gap: 5px; margin-top: auto; }
.m-block  { height: 16px; border-radius: 3px; background: rgba(41,151,255,.18); }
.m-block:nth-child(2) { background: rgba(41,151,255,.32); }
.m-block:nth-child(3) { background: rgba(0,170,120,.2); }




.hero-text { display: flex; flex-direction: column; align-items: center; }




.hero-eyebrow { font-size: 17px; font-weight: 600; color: #f5f5f7; margin-bottom: 10px; }
.hero-title {
  font-size: clamp(40px,7vw,80px); font-weight: 700;
  letter-spacing: -.04em; line-height: 1.05;
  color: #f5f5f7; margin-bottom: 18px;
}
.hero-desc { font-size: 19px; font-weight: 300; color: #6e6e73; line-height: 1.6; margin-bottom: 36px; }
.hero-desc strong { color: #f5f5f7; font-weight: 400; }
.hero-btns { display: flex; gap: 16px; flex-wrap: wrap; justify-content: center; }
.btn-primary {
  font-size: 17px; font-weight: 500; color: #fff;
  background: #0066cc; padding: 14px 28px; border-radius: 100px;
  transition: background .2s;
}
.btn-primary:hover { background: #0077ed; }
.btn-ghost { font-size: 17px; font-weight: 500; color: #2997ff; padding: 14px 0; }
.btn-ghost:hover { text-decoration: underline; }
</style>
