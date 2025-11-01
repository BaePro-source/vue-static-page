<template>
  <div :class="['app', isDark ? 'theme-dark' : 'theme-light']">
    <!-- 상단 네비게이션 -->
    <header class="nav">
      <div class="brand" @click="scrollTo('#hero')" role="button" aria-label="홈으로">
        <!-- MoonIcon 대체: 단순 SVG -->
        <svg
            v-if="isDark"
            width="20"
            height="20"
            viewBox="0 0 24 24"
            aria-hidden="true"
            style="margin-right:8px"
        >
          <path fill="currentColor" d="M12 2a9.99 9.99 0 0 0 0 20c5.52 0 10-4.48 10-10 0-4.41-2.86-8.15-6.84-9.46A8 8 0 0 1 12 2z"/>
        </svg>
        <svg
            v-else
            width="20"
            height="20"
            viewBox="0 0 24 24"
            aria-hidden="true"
            style="margin-right:8px"
        >
          <path fill="currentColor" d="M20 15.31A8 8 0 1 1 8.69 4 9.99 9.99 0 1 0 20 15.31z"/>
        </svg>
        <span>한가위 한 페이지</span>
      </div>
      <nav class="links">
        <a href="#about">소개</a>
        <a href="#foods">전통 음식</a>
        <a href="#games">전통 놀이</a>
        <a href="#gallery">갤러리</a>
      </nav>
      <button class="toggle" @click="toggleTheme" :aria-pressed="isDark" aria-label="달 밝기 전환">
        <span v-if="isDark">🌕 밝게</span>
        <span v-else>🌙 어둡게</span>
      </button>
    </header>

    <!-- 히어로 -->
    <section id="hero" class="hero">
      <div class="lanterns">
        <div
            v-for="n in 5"
            :key="n"
            class="lantern"
            :style="{ animationDelay: (n * 0.6) + 's' }"
            aria-hidden="true"
        ></div>
      </div>
      <div class="hero-inner">
        <h1>한가위, 보름달처럼 가득 찬 <em>마음</em></h1>
        <p class="subtitle">
          가족과 이웃에게 온기를 전하는 날, <strong>추석</strong>의 이야기를 담았습니다.
        </p>
        <div class="cta">
          <a class="btn" href="#about">바로 보기</a>
          <button class="btn ghost" @click="toNext">아래로 스크롤</button>
        </div>
        <!-- 카운트다운 컴포넌트 -->
        <Countdown target="2025-09-07T00:00:00" label="올해 추석까지" />
      </div>
      <div class="moon-wrap">
        <svg class="moon" viewBox="0 0 100 100" aria-hidden="true">
          <defs>
            <radialGradient id="g" cx="50%" cy="45%" r="60%">
              <stop offset="0%" :stop-color="cssVars.moonCore" />
              <stop offset="100%" :stop-color="cssVars.moonRing" />
            </radialGradient>
          </defs>
          <circle cx="50" cy="50" r="35" fill="url(#g)"/>
        </svg>
        <div class="cloud c1"></div>
        <div class="cloud c2"></div>
      </div>
    </section>

    <!-- 소개 -->
    <section id="about" class="section about">
      <h2>풍성한 마음을 나누는 날</h2>
      <p>
        한가위(추석)는 음력 8월 15일로, 한 해의 수확에 감사하고 가족·이웃과 정을 나누는 한국의 대표 명절입니다.
        성묘와 차례, 나눔과 놀이, 그리고 맛있는 음식이 어우러져 모두의 얼굴에 보름달 같은 미소가 번지는 날입니다.
      </p>
      <ul class="features">
        <li>
          <span class="icon">🕯️</span>
          <div>
            <strong>정성</strong>
            <p>조상께 감사드리는 마음과 서로를 위한 배려를 담아요.</p>
          </div>
        </li>
        <li>
          <span class="icon">🤝</span>
          <div>
            <strong>나눔</strong>
            <p>이웃과 음식을 나누고 덕담을 전하며 따뜻함을 나눠요.</p>
          </div>
        </li>
        <li>
          <span class="icon">🎎</span>
          <div>
            <strong>흥겨움</strong>
            <p>강강술래, 윷놀이 등 전통 놀이로 온 세대가 어울려요.</p>
          </div>
        </li>
      </ul>
    </section>

    <!-- 전통 음식 -->
    <section id="foods" class="section grid two">
      <div class="text">
        <h2>전통 음식</h2>
        <p class="lead">
          제철 재료로 빚은 음식은 <em>감사</em>와 <em>정성</em>을 담는 그릇입니다.
        </p>
        <ul class="cards">
          <li>
            <h3>송편</h3>
            <p>솔잎 향 머금은 반달떡. 깨·콩·밤 소를 넣어 빚어요.</p>
            <small>#쫄깃 #솔향</small>
          </li>
          <li>
            <h3>전(煎)</h3>
            <p>부침개·동그랑땡·배추전 등 다양한 전으로 상을 풍성하게.</p>
            <small>#노릇노릇 #풍성한상</small>
          </li>
          <li>
            <h3>나물</h3>
            <p>시금치·고사리·도라지 등 산해진미의 담백한 조화.</p>
            <small>#제철 #균형</small>
          </li>
        </ul>
      </div>
      <figure class="art">
        <div class="plate">
          <div class="rice"></div>
          <div class="piece p1"></div>
          <div class="piece p2"></div>
          <div class="piece p3"></div>
          <div class="leaf l1"></div>
          <div class="leaf l2"></div>
        </div>
        <figcaption>간단한 CSS 일러스트로 표현한 한가위 한 상</figcaption>
      </figure>
    </section>

    <!-- 전통 놀이 -->
    <section id="games" class="section games">
      <h2>전통 놀이</h2>
      <div class="chips">
        <span class="chip"><span class="emoji" aria-hidden="true">🌀</span><span>강강술래</span></span>
        <span class="chip"><span class="emoji" aria-hidden="true">🪵</span><span>윷놀이</span></span>
        <span class="chip"><span class="emoji" aria-hidden="true">🤼</span><span>씨름</span></span>
        <span class="chip"><span class="emoji" aria-hidden="true">🪢</span><span>줄다리기</span></span>
        <span class="chip"><span class="emoji" aria-hidden="true">🪁</span><span>연날리기</span></span>
      </div>
      <p class="tip">작은 마당이나 거실에서도 규칙을 단순화해 충분히 즐길 수 있어요!</p>
    </section>

    <!-- 갤러리 -->
    <section id="gallery" class="section gallery">
      <h2>갤러리</h2>
      <div class="grid four">
        <figure v-for="(g, i) in gallery" :key="i" class="tile">
          <img :src="g.src" :alt="g.alt" loading="lazy" />
          <figcaption>{{ g.alt }}</figcaption>
        </figure>
      </div>
    </section>

    <!-- 푸터 -->
    <footer class="footer">
      <p>© {{ year }} 한가위 한 페이지 · 보름달처럼 넉넉한 하루 되세요.</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, defineComponent } from 'vue'

/** 다크모드 */
const isDark = ref<boolean>(window.matchMedia?.('(prefers-color-scheme: dark)').matches ?? false)
const toggleTheme = () => (isDark.value = !isDark.value)

/** 스크롤 유틸 */
const scrollTo = (sel: string) => {
  document.querySelector(sel)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}
const toNext = () => scrollTo('#about')

/** 연도 */
const year = new Date().getFullYear()

/** 갤러리(데모용) */
type Photo = { src: string; alt: string }
const gallery = ref<Photo[]>([
  { src: 'https://images.unsplash.com/photo-1545249390-6bdfa286032f?q=80&w=1200&auto=format&fit=crop', alt: '가을 하늘과 달' },
  { src: 'https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?q=80&w=1200&auto=format&fit=crop', alt: '황금 들판' },
  { src: 'https://images.unsplash.com/photo-1500534314209-a25ddb2bd429?q=80&w=1200&auto=format&fit=crop', alt: '따뜻한 등불' },
  { src: 'https://images.unsplash.com/photo-1500534623283-312aade485b7?q=80&w=1200&auto=format&fit=crop', alt: '가족의 시간' },
])

/** 접근성: 시스템 테마 변경 감지 */
onMounted(() => {
  const mq = window.matchMedia?.('(prefers-color-scheme: dark)')
  const cb = (e: MediaQueryListEvent) => (isDark.value = e.matches)
  mq?.addEventListener?.('change', cb)
})

/** CSS 변수 바인딩용(그라디언트 스톱 컬러) */
const cssVars = {
  get moonCore() { return getComputedStyle(document.documentElement).getPropertyValue('--moon-core') || '#fff0c2' },
  get moonRing() { return getComputedStyle(document.documentElement).getPropertyValue('--moon-ring') || '#f59e0b44' },
}

/** JSX 없이 템플릿을 쓰는 로컬 컴포넌트 */
const Countdown = defineComponent({
  name: 'Countdown',
  props: {
    target: { type: String, required: true },
    label: { type: String, default: '남은 시간' }
  },
  setup(props) {
    const remain = ref<string>('계산 중…')
    const t = new Date(props.target).getTime()
    const tick = () => {
      const now = Date.now()
      const diff = Math.max(0, t - now)
      const d = Math.floor(diff / (1000 * 60 * 60 * 24))
      const h = Math.floor((diff / (1000 * 60 * 60)) % 24)
      const m = Math.floor((diff / (1000 * 60)) % 60)
      const s = Math.floor((diff / 1000) % 60)
      remain.value = `${d}일 ${h}시간 ${m}분 ${s}초`
    }
    onMounted(() => {
      tick()
      id = window.setInterval(tick, 1000)
    })
    return { remain, props }
  },
  template: `
    <div class="countdown" role="status" aria-live="polite">
      <small class="count-label">{{ props.label }}</small>
      <div class="count-value">{{ remain }}</div>
    </div>
  `
})
</script>

<style scoped>
:root {
  --bg: #0b1020;
  --fg: #e6edf6;
  --muted: #b6c2d6;
  --primary: #ffd166;
  --accent: #7cc6ff;
  --surface: #151b2e;

  --moon-core: #fff6d5;
  --moon-ring: #ffd16644;
}

.theme-light {
  --bg: #f8fafc;
  --fg: #0b1020;
  --muted: #4b5563;
  --surface: #ffffff;
  --accent: #2563eb;
  --primary: #f59e0b;

  --moon-core: #fff0c2;
  --moon-ring: #f59e0b44;
}

.app {
  background: var(--bg);
  color: var(--fg);
  min-height: 100dvh;
  line-height: 1.6;
  font-synthesis-weight: none;
}

/* NAV */
.nav {
  position: sticky;
  top: 0;
  z-index: 10;
  display: grid;
  grid-template-columns: 1fr auto auto;
  gap: 12px;
  align-items: center;
  padding: 12px 20px;
  background: color-mix(in srgb, var(--bg) 85%, transparent);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid color-mix(in srgb, var(--fg) 10%, transparent);
}
.brand {
  display: inline-flex;
  align-items: center;
  font-weight: 700;
  letter-spacing: .4px;
  cursor: pointer;
}
.links {
  display: none;
  gap: 14px;
}
.links a {
  color: var(--muted);
  text-decoration: none;
  font-weight: 600;
}
.links a:hover { color: var(--fg); }
.toggle {
  border: 1px solid color-mix(in srgb, var(--fg) 15%, transparent);
  background: var(--surface);
  color: var(--fg);
  padding: 8px 12px;
  border-radius: 999px;
  cursor: pointer;
}
@media (min-width: 860px) {
  .links { display: inline-flex; }
}

/* HERO */
.hero {
  position: relative;
  overflow: hidden;
  padding: 96px 20px 72px;
  isolation: isolate;
}
.hero-inner {
  max-width: 980px;
  margin: 0 auto;
  text-align: center;
}
.hero h1 {
  font-size: clamp(28px, 4vw, 52px);
  letter-spacing: .3px;
}
.hero .subtitle {
  color: var(--muted);
  margin: 10px auto 22px;
  max-width: 680px;
}
.cta {
  display: inline-flex;
  gap: 10px;
  margin-bottom: 18px;
}
.btn {
  padding: 10px 16px;
  border-radius: 12px;
  border: 1px solid color-mix(in srgb, var(--fg) 12%, transparent);
  background: var(--primary);
  color: #1f2937;
  font-weight: 700;
  cursor: pointer;
  text-decoration: none;
}
.btn.ghost {
  background: transparent;
  color: var(--fg);
}
.moon-wrap {
  position: absolute;
  inset: 0 0 auto 50%;
  translate: -50% -10%;
  pointer-events: none;
  z-index: -1;
}
.moon {
  width: min(56vmin, 560px);
  filter: drop-shadow(0 0 30px color-mix(in srgb, var(--primary) 40%, transparent));
}

/* 구름 */
.cloud {
  position: absolute; top: 35%; left: 50%;
  width: 180px; height: 60px; border-radius: 999px;
  background: color-mix(in srgb, var(--fg) 10%, transparent);
  filter: blur(2px);
  animation: floatX 26s linear infinite;
}
.cloud.c1 { top: 32%; left: 18%; width: 240px; height: 70px; animation-duration: 32s; }
.cloud.c2 { top: 48%; left: 68%; width: 220px; height: 64px; animation-duration: 28s; }
@keyframes floatX {
  from { transform: translateX(-40vw); }
  to { transform: translateX(40vw); }
}

/* 등(랜턴) */
.lanterns { position: absolute; inset: 0; pointer-events: none; }
.lantern {
  --rand: 0.3;
  position: absolute;
  left: calc(10% + 80% * var(--rand, 0));
  top: -60px;
  width: 14px; height: 18px;
  background: radial-gradient(circle at 50% 30%, #ffd166 0 40%, #ffb703 41% 100%);
  border-radius: 4px 4px 10px 10px;
  box-shadow: 0 0 10px #ffd166aa, 0 0 20px #ffd16655;
  animation: fall 12s linear infinite, swing 2.4s ease-in-out infinite alternate;
}
.lantern::after {
  content: '';
  position: absolute; inset: -4px; border-top: 2px solid #ffd16666;
}
@keyframes fall { from { transform: translateY(-10vh); } to { transform: translateY(110vh); } }
@keyframes swing { from { transform: rotate(-4deg); } to { transform: rotate(4deg); } }

/* COUNTDOWN */
.countdown {
  display: inline-grid;
  gap: 4px;
  padding: 8px 12px;
  border-radius: 10px;
  margin-top: 12px;
  background: color-mix(in srgb, var(--surface) 80%, transparent);
  border: 1px solid color-mix(in srgb, var(--fg) 12%, transparent);
}
.count-label { color: var(--muted); }
.count-value { font-weight: 800; letter-spacing: .5px; }

/* 공통 섹션 */
.section { padding: 72px 20px; }
.section > h2 {
  text-align: center;
  margin: 0 auto 14px;
  font-size: clamp(22px, 3vw, 32px);
}
.section > p.lead {
  text-align: center;
  margin: 0 auto 24px;
  max-width: 720px;
  color: var(--muted);
}

/* 소개 */
.about { max-width: 980px; margin: 0 auto; }
.features { display: grid; gap: 16px; margin-top: 22px; }
.features li {
  display: grid; grid-template-columns: 40px 1fr; gap: 12px;
  padding: 12px; border-radius: 12px;
  background: color-mix(in srgb, var(--surface) 80%, transparent);
  border: 1px solid color-mix(in srgb, var(--fg) 10%, transparent);
}
.features .icon { font-size: 22px; }

/* 음식 섹션 */
.grid.two { display: grid; gap: 26px; max-width: 1100px; margin: 0 auto; }
@media (min-width: 960px) {
  .grid.two { grid-template-columns: 1.1fr .9fr; align-items: center; }
}
.cards { display: grid; gap: 12px; margin-top: 18px; }
.cards li {
  padding: 14px; border-radius: 12px;
  background: color-mix(in srgb, var(--surface) 80%, transparent);
  border: 1px solid color-mix(in srgb, var(--fg) 10%, transparent);
}
.cards h3 { margin: 0 0 4px; }
.cards small { color: var(--muted); }

/* CSS 일러스트 */
.art { text-align: center; }
.plate {
  --plate: color-mix(in srgb, var(--fg) 8%, transparent);
  width: clamp(240px, 40vmin, 360px);
  height: clamp(240px, 40vmin, 360px);
  margin: 0 auto;
  border-radius: 50%;
  background: radial-gradient(circle at 50% 50%, var(--plate) 0 70%, transparent 71% 100%);
  position: relative;
}
.rice { position: absolute; inset: 22% 22%; border-radius: 50%; background: radial-gradient(circle at 40% 40%, #fff 0 60%, #ddd 61% 100%); }
.piece { position: absolute; width: 46px; height: 26px; border-radius: 16px; }
.p1 { background: #f59e0b; left: 30%; top: 28%; rotate: -12deg; }
.p2 { background: #22c55e; right: 26%; top: 42%; rotate: 8deg; }
.p3 { background: #ef4444; left: 42%; bottom: 26%; rotate: 18deg; }
.leaf { position: absolute; width: 36px; height: 18px; border-radius: 18px 2px 18px 2px; background: #10b981; }
.l1 { left: 18%; top: 44%; rotate: -20deg; }
.l2 { right: 18%; top: 30%; rotate: 14deg; }
figcaption { color: var(--muted); margin-top: 10px; }

/* 놀이 */
.games { text-align: center; }
.chips { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; margin-top: 16px; }
.chip {
  display: inline-flex; align-items: center; gap: 6px;
  padding: 8px 12px; border-radius: 999px; font-weight: 600;
  background: color-mix(in srgb, var(--surface) 80%, transparent);
  border: 1px solid color-mix(in srgb, var(--fg) 12%, transparent);
}
.chip .emoji { filter: drop-shadow(0 1px 0 color-mix(in srgb, var(--fg) 10%, transparent)); }
.tip { color: var(--muted); margin-top: 12px; }

/* 갤러리 */
.gallery { max-width: 1100px; margin: 0 auto; }
.grid.four {
  display: grid; gap: 12px;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
}
.tile {
  border-radius: 12px; overflow: hidden;
  background: color-mix(in srgb, var(--surface) 80%, transparent);
  border: 1px solid color-mix(in srgb, var(--fg) 10%, transparent);
}
.tile img { width: 100%; height: 180px; object-fit: cover; display: block; }
.tile figcaption { padding: 8px 10px; color: var(--muted); }

/* 푸터 */
.footer { text-align: center; padding: 40px 20px 60px; color: var(--muted); }
</style>
