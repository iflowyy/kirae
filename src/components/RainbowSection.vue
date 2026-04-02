<template>
  <section class="rb-section">
    <div class="rb-aurora">
      <div class="aurora-layer l1"></div>
      <div class="aurora-layer l2"></div>
      <div class="aurora-layer l3"></div>
      <div class="aurora-layer l4"></div>
      <div class="aurora-layer l5"></div>
      <div class="aurora-fade-bottom"></div>
      <div class="aurora-fade-top"></div>
    </div>

    <div class="rb-content">
      <div class="">
       
      </div>
   
     
    </div>
  </section>
</template>

<style scoped>
.rb-section {
  position: relative;
  background: #000;
  overflow: hidden;
  min-height: 500px;
}

.rb-aurora {
  position: absolute;
  inset: 0;
  overflow: hidden;
}

.aurora-layer {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0;
  animation: auroraFade 0.8s ease forwards;
}

@keyframes auroraFade {
  to { opacity: 1; }
}

.l1 {
  width: 55%; height: 70%;
  left: -8%; bottom: -10%;
  background: radial-gradient(ellipse at center,
    #c84b11 0%, #b5281c 35%, transparent 72%);
  animation-delay: .05s;
}
.l2 {
  width: 60%; height: 80%;
  left: 10%; bottom: -15%;
  background: radial-gradient(ellipse at center,
    #c0186e 0%, #a0107a 30%, transparent 68%);
  animation-delay: .1s;
}
.l3 {
  width: 65%; height: 90%;
  left: 22%; bottom: -20%;
  background: radial-gradient(ellipse at center,
    #7b2fbe 0%, #5e35ca 28%, transparent 65%);
  animation-delay: .15s;
}
.l4 {
  width: 60%; height: 85%;
  right: 5%; bottom: -18%;
  background: radial-gradient(ellipse at center,
    #1a6fe0 0%, #2d5be3 25%, transparent 65%);
  animation-delay: .2s;
}
.l5 {
  width: 50%; height: 75%;
  right: -10%; bottom: -12%;
  background: radial-gradient(ellipse at center,
    #0db8d1 0%, #0dcfb2 28%, #0dd68a 48%, transparent 70%);
  animation-delay: .25s;
}

.aurora-fade-top {
  position: absolute; top: 0; left: 0; right: 0;
  height: 45%;
  background: linear-gradient(to bottom, #000 0%, transparent 100%);
  pointer-events: none;
}
.aurora-fade-bottom {
  position: absolute; bottom: 0; left: 0; right: 0;
  height: 40%;
  background: linear-gradient(to top, #000 0%, transparent 100%);
  pointer-events: none;
}

.rb-content {
  position: relative; z-index: 2;
  max-width: 600px;
  margin: 0 auto;
  padding: 80px 32px 100px;
  text-align: left;
}

.tag-pill {
  display: inline-flex; align-items: center; gap: 8px;
  background: rgba(255,255,255,.07);
  border: 1px solid rgba(255,255,255,.1);
  border-radius: 100px; padding: 7px 16px;
  margin-bottom: 32px;
}
.pill-dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: rgba(255,255,255,.5);
}
.pill-sep { color: rgba(255,255,255,.18); font-size: 16px; }

.rb-label {
  font-size: 17px; font-weight: 600;
  color: #f5f5f7; margin-bottom: 8px;
  letter-spacing: -0.01em;
}
.rb-title {
  font-size: clamp(32px,5vw,52px); font-weight: 700;
  letter-spacing: -.03em; color: #f5f5f7;
  margin-bottom: 22px; line-height: 1.05;
}
.rb-desc {
  font-size: 19px; font-weight: 300;
  color: #86868b;
  line-height: 1.7;
}
.rb-desc em {
  font-style: normal;
  color: #c8c8cc;
  font-weight: 400;
}
</style>