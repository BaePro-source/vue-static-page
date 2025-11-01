<template>
  <div :class="['app', isDark ? 'theme-dark' : 'theme-light']">
    <!-- NAV -->
    <header class="nav">
      <div class="brand" @click="scrollTo('#hero')">
        <span class="logo" aria-hidden="true">🌕</span>
        <span>한가위 한 페이지</span>
      </div>
      <nav class="links">
        <a href="#about">소개</a>
        <a href="#foods">전통 음식</a>
        <a href="#games">전통 놀이</a>
        <a href="#gallery">갤러리</a>
        <a href="#timeline">일정</a>
        <a href="#faq">FAQ</a>
      </nav>
      <button class="toggle" @click="toggleTheme" :aria-pressed="isDark">
        <span v-if="isDark">☀️ 밝게</span>
        <span v-else>🌙 어둡게</span>
      </button>
    </header>

    <!-- HERO -->
    <section id="hero" class="hero">
      <div class="bg-moon" aria-hidden="true">
        <svg viewBox="0 0 100 100">
          <defs>
            <radialGradient id="g" cx="50%" cy="45%" r="60%">
              <stop offset="0%" stop-color="var(--moon-core)" />
              <stop offset="100%" stop-color="var(--moon-ring)" />
            </radialGradient>
          </defs>
          <circle cx="50" cy="50" r="35" fill="url(#g)"/>
        </svg>
        <div class="cloud c1"></div>
        <div class="cloud c2"></div>
      </div>

      <div class="hero-inner">
        <h1>한가위, 보름달처럼 가득 찬 <em>마음</em></h1>
        <p class="subtitle">
          가족과 이웃에게 온기를 전하는 날, <strong>추석</strong>의 이야기를 담았습니다.
        </p>
        <div class="cta">
          <a class="btn" href="#about">둘러보기</a>
          <button class="btn ghost" @click="toNext">아래로 스크롤</button>
        </div>
        <Countdown target="2025-09-07T00:00:00" label="올해 추석까지" />
      </div>

      <!-- 랜턴 데코 -->
      <div class="lanterns" aria-hidden="true">
        <div v-for="n in 6" :key="n" class="lantern" :style="{ animationDelay: (n * 0.7) + 's' }"></div>
      </div>
    </section>

    <!-- 소개 -->
    <section id="about" class="section about">
      <h2>풍성한 마음을 나누는 날</h2>
      <p class="lead">
        한가위(추석)는 한 해의 수확에 감사하고, 정을 나누는 한국의 대표 명절입니다.
        성묘와 차례, 나눔과 놀이, 맛있는 음식이 어우러져 모두의 얼굴에 보름달 같은 미소가 번지는 날입니다.
      </p>
      <ul class="features">
        <li>
          <span class="icon">🕯️</span>
          <div>
            <strong>정성</strong>
            <p>조상께 감사드리는 마음과 서로를 위한 배려를 담습니다.</p>
          </div>
        </li>
        <li>
          <span class="icon">🤝</span>
          <div>
            <strong>나눔</strong>
            <p>이웃과 음식을 나누고 덕담을 전하며 따뜻함을 나눕니다.</p>
          </div>
        </li>
        <li>
          <span class="icon">🎎</span>
          <div>
            <strong>흥겨움</strong>
            <p>강강술래, 윷놀이 등 전통 놀이로 온 세대가 어울립니다.</p>
          </div>
        </li>
      </ul>
    </section>

    <!-- 전통 음식 -->
    <section id="foods" class="section foods grid two">
      <div class="text">
        <h2>전통 음식</h2>
        <p class="lead">제철 재료로 빚은 음식은 <em>감사</em>와 <em>정성</em>을 담는 그릇입니다.</p>
        <ul class="cards">
          <li v-for="f in foods" :key="f.name">
            <h3>{{ f.name }}</h3>
            <p>{{ f.desc }}</p>
            <small>{{ f.tags }}</small>
          </li>
        </ul>
      </div>
      <!-- 간단 CSS 일러스트 -->
      <figure class="art">
        <div class="plate">
          <div class="rice"></div>
          <div class="piece p1"></div>
          <div class="piece p2"></div>
          <div class="piece p3"></div>
          <div class="leaf l1"></div>
          <div class="leaf l2"></div>
        </div>
        <figcaption>솔잎 향 가득한 한가위 한 상</figcaption>
      </figure>
    </section>

    <!-- 전통 놀이 -->
    <section id="games" class="section games">
      <h2>전통 놀이</h2>
      <div class="chips">
        <span v-for="g in games" :key="g.text" class="chip">
          <span class="emoji" aria-hidden="true">{{ g.emoji }}</span>
          <span>{{ g.text }}</span>
        </span>
      </div>
      <p class="tip">작은 공간에서도 규칙을 단순화하면 충분히 즐길 수 있습니다.</p>
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

    <!-- 일정 타임라인 -->
    <section id="timeline" class="section timeline">
      <h2>한가위 일정</h2>
      <ol class="steps">
        <li v-for="(t, i) in timeline" :key="i">
          <div class="dot" aria-hidden="true"></div>
          <div class="content">
            <strong>{{ t.title }}</strong>
            <p class="muted">{{ t.time }}</p>
            <p>{{ t.desc }}</p>
          </div>
        </li>
      </ol>
    </section>

    <!-- FAQ 아코디언 -->
    <section id="faq" class="section faq">
      <h2>자주 묻는 질문</h2>
      <details v-for="(q, i) in faq" :key="i" class="qa">
        <summary>{{ q.q }}</summary>
        <p>{{ q.a }}</p>
      </details>
    </section>

    <!-- 푸터 -->
    <footer class="footer">
      <form class="subscribe" @submit.prevent="onSubscribe">
        <label for="email" class="muted">소식받기</label>
        <input id="email" v-model="email" type="email" required placeholder="you@example.com" />
        <button class="btn">구독</button>
      </form>
      <p class="muted">© {{ year }} 한가위 한 페이지 · 보름달처럼 넉넉한 하루 되세요.</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, defineComponent } from 'vue'

/* 테마 */
const isDark = ref<boolean>(
    window.matchMedia?.('(prefers-color-scheme: dark)').matches ?? false
)
const toggleTheme = () => (isDark.value = !isDark.value)

/* 스크롤 */
const scrollTo = (sel: string) =>
    document.querySelector(sel)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
const toNext = () => scrollTo('#about')

/* 연도 */
const year = new Date().getFullYear()

/* 전통 음식/놀이/갤러리 데이터 */
type Food = { name: string; desc: string; tags: string }
type Game = { text: string; emoji: string }
type Photo = { src: string; alt: string }
type Step = { title: string; time: string; desc: string }
type QA = { q: string; a: string }

const foods = ref<Food[]>([
  { name: '송편', desc: '솔잎 향 머금은 반달떡. 깨·콩·밤 소를 넣어 빚습니다.', tags: '#쫄깃 #솔향' },
  { name: '전(煎)', desc: '동그랑땡·배추전 등 다양한 전으로 상을 풍성하게.', tags: '#노릇노릇 #풍성한상' },
  { name: '나물', desc: '시금치·고사리·도라지 등 담백한 조화.', tags: '#제철 #균형' }
])

const games = ref<Game[]>([
  { text: '강강술래', emoji: '🌀' },
  { text: '윷놀이', emoji: '🪵' },
  { text: '씨름', emoji: '🤼' },
  { text: '줄다리기', emoji: '🪢' },
  { text: '연날리기', emoji: '🪁' }
])

const gallery = ref<Photo[]>([
  { src: 'https://images.unsplash.com/photo-1545249390-6bdfa286032f?q=80&w=1200&auto=format&fit=crop', alt: '가을 하늘과 달' },
  { src: 'https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?q=80&w=1200&auto=format&fit=crop', alt: '황금 들판' },
  { src: 'https://images.unsplash.com/photo-1500534314209-a25ddb2bd429?q=80&w=1200&auto=format&fit=crop', alt: '따뜻한 등불' },
  { src: 'https://images.unsplash.com/photo-1500534623283-312aade485b7?q=80&w=1200&auto=format&fit=crop', alt: '가족의 시간' }
])

const timeline = ref<Step[]>([
  { title: '성묘·차례 준비', time: '아침', desc: '정성껏 차림을 준비하고 마음을 가다듬습니다.' },
  { title: '차례 지내기', time: '오전', desc: '조상께 감사의 마음을 전합니다.' },
  { title: '함께 식사', time: '점심', desc: '송편과 전, 나물로 풍성한 한 상을 나눕니다.' },
  { title: '전통 놀이', time: '오후', desc: '세대가 함께 어울려 웃음을 나눕니다.' },
  { title: '달맞이', time: '저녁', desc: '보름달을 바라보며 소원을 빕니다.' }
])

const faq = ref<QA[]>([
  { q: '이미지는 상업적으로 사용해도 되나요?', a: '데모 이미지는 Unsplash 링크입니다. 실제 배포 시에는 직접 촬영하거나 라이선스가 확실한 이미지를 사용해 주세요.' },
  { q: '색상이나 글꼴을 바꾸려면?', a: '아래 CSS 변수(--bg, --fg, --primary 등)를 변경하시면 전체 톤이 바뀝니다.' },
  { q: '다크모드 기본값을 고정할 수 있나요?', a: 'isDark 초기값을 true/false로 지정하면 됩니다.' }
])

/* 구독 폼 (데모) */
const email = ref<string>('')
const onSubscribe = () => {
  // 실제 프로젝트에서는 서버 API 연동
  alert(`구독해주셔서 감사합니다! (${email.value})`)
  email.value = ''
}

/* 카운트다운 로컬 컴포넌트 */
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

    let intervalId: number | undefined
    onMounted(() => { tick(); intervalId = window.setInterval(tick, 1000) })
    onUnmounted(() => { if (intervalId !== undefined) window.clearInterval(intervalId) })

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
/* 색상 테마 */
:root {
  --bg: #0b1020;
  --fg: #e6edf6;
  --muted: #b6c2d6;
  --surface: #151b2e;
  --primary: #ffd166;
  --accent: #7cc6ff;

  --moon-core: #fff6d5;
  --moon-ring: #ffd16644;
}
.theme-light {
  --bg: #f8fafc;
  --fg: #0b1020;
  --muted: #4b5563;
  --surface: #ffffff;
  --primary: #f59e0b;
  --accent: #2563eb;

  --moon-core: #fff0c2;
  --moon-ring: #f59e0b44;
}

/* 기본 레이아웃 */
.app { background: var(--bg); color: var(--fg); min-height: 100dvh; }
.nav {
  position: sticky; top: 0; z-index: 10;
  display: grid; grid-template-columns: 1fr auto auto; gap: 12px; align-items: center;
  padding: 12px 20px; background: color-mix(in srgb, var(--bg) 85%, transparent);
  backdrop-filter: blur(10px); border-bottom: 1px solid color-mix(in srgb, var(--fg) 10%, transparent);
}
.brand { display: inline-flex; align-items: center; gap: 8px; font-weight: 700; cursor: pointer; }
.logo { filter: drop-shadow(0 0 6px color-mix(in srgb, var(--primary) 60%, transparent)); }
.links { display: none; gap: 14px; }
.links a { color: var(--muted); text-decoration: none; font-weight: 600; }
.links a:hover { color: var(--fg); }
.toggle { border: 1px solid color-mix(in srgb, var(--fg) 15%, transparent); background: var(--surface); color: var(--fg); padding: 8px 12px; border-radius: 999px; cursor: pointer; }
@media (min-width: 860px) { .links { display: inline-flex; } }

/* HERO */
.hero { position: relative; overflow: hidden; padding: 96px 20px 80px; text-align: center; }
.hero-inner { max-width: 980px; margin: 0 auto; }
.hero h1 { font-size: clamp(28px, 4vw, 52px); }
.subtitle { color: var(--muted); max-width: 680px; margin: 10px auto 22px; }
.cta { display: inline-flex; gap: 10px; margin-bottom: 18px; }
.btn { padding: 10px 16px; border-radius: 12px; border: 1px solid color-mix(in srgb, var(--fg) 12%, transparent); background: var(--primary); color: #1f2937; font-weight: 700; cursor: pointer; text-decoration: none; }
.btn.ghost { background: transparent; color: var(--fg); }

/* 달/구름 배경 */
.bg-moon { position: absolute; inset: -10% 0 auto 50%; translate: -50% -6%; pointer-events: none; z-index: -1; }
.bg-moon svg { width: min(56vmin, 560px); filter: drop-shadow(0 0 30px color-mix(in srgb, var(--primary) 40%, transparent)); }
.cloud { position: absolute; top: 35%; left: 50%; width: 180px; height: 60px; border-radius: 999px; background: color-mix(in srgb, var(--fg) 10%, transparent); filter: blur(2px); animation: floatX 26s linear infinite; }
.cloud.c1 { top: 32%; left: 18%; width: 240px; height: 70px; animation-duration: 32s; }
.cloud.c2 { top: 48%; left: 68%; width: 220px; height: 64px; animation-duration: 28s; }
@keyframes floatX { from { transform: translateX(-40vw); } to { transform: translateX(40vw); } }

/* 랜턴 */
.lanterns { position: absolute; inset: 0; pointer-events: none; }
.lantern {
  position: absolute; left: calc(10% + 80% * var(--rand, 0.2)); top: -60px;
  width: 14px; height: 18px; border-radius: 4px 4px 10px 10px;
  background: radial-gradient(circle at 50% 30%, #ffd166 0 40%, #ffb703 41% 100%);
  box-shadow: 0 0 10px #ffd166aa, 0 0 20px #ffd16655;
  animation: fall 12s linear infinite, swing 2.4s ease-in-out infinite alternate;
}
.lantern::after { content: ''; position: absolute; inset: -4px; border-top: 2px solid #ffd16666; }
@keyframes fall { from { transform: translateY(-10vh); } to { transform: translateY(110vh); } }
@keyframes swing { from { transform: rotate(-4deg); } to { transform: rotate(4deg); } }

/* 공통 섹션 */
.section { padding: 72px 20px; }
.section > h2 { text-align: center; margin-bottom: 14px; font-size: clamp(22px, 3vw, 32px); }
.section > p.lead { text-align: center; margin: 0 auto 24px; max-width: 720px; color: var(--muted); }

/* 소개 */
.about { max-width: 980px; margin: 0 auto; }
.features { display: grid; gap: 16px; margin-top: 22px; }
.features li { display: grid; grid-template-columns: 40px 1fr; gap: 12px; padding: 12px; border-radius: 12px; background: color-mix(in srgb, var(--surface) 80%, transparent); border: 1px solid color-mix(in srgb, var(--fg) 10%, transparent); }
.features .icon { font-size: 22px; }

/* 음식 섹션 */
.grid.two { display: grid; gap: 26px; max-width: 1100px; margin: 0 auto; }
@media (min-width: 960px) { .grid.two { grid-template-columns: 1.1fr .9fr; align-items: center; } }
.cards { display: grid; gap: 12px; margin-top: 18px; }
.cards li { padding: 14px; border-radius: 12px; background: color-mix(in srgb, var(--surface) 80%, transparent); border: 1px solid color-mix(in srgb, var(--fg) 10%, transparent); }
.cards h3 { margin: 0 0 4px; }
.cards small { color: var(--muted); }

/* CSS 일러스트 */
.art { text-align: center; }
.plate { --plate: color-mix(in srgb, var(--fg) 8%, transparent); width: clamp(240px, 40vmin, 360px); height: clamp(240px, 40vmin, 360px); margin: 0 auto; border-radius: 50%; background: radial-gradient(circle at 50% 50%, var(--plate) 0 70%, transparent 71% 100%); position: relative; }
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
.chip { display: inline-flex; align-items: center; gap: 6px; padding: 8px 12px; border-radius: 999px; font-weight: 600; background: color-mix(in srgb, var(--surface) 80%, transparent); border: 1px solid color-mix(in srgb, var(--fg) 12%, transparent); }
.chip .emoji { filter: drop-shadow(0 1px 0 color-mix(in srgb, var(--fg) 10%, transparent)); }
.tip { color: var(--muted); margin-top: 12px; }

/* 갤러리 */
.gallery { max-width: 1100px; margin: 0 auto; }
.grid.four { display: grid; gap: 12px; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); }
.tile { border-radius: 12px; overflow: hidden; background: color-mix(in srgb, var(--surface) 80%, transparent); border: 1px solid color-mix(in srgb, var(--fg) 10%, transparent); }
.tile img { width: 100%; height: 180px; object-fit: cover; display: block; }
.tile figcaption { padding: 8px 10px; color: var(--muted); }

/* 타임라인 */
.timeline { max-width: 820px; margin: 0 auto; }
.steps { list-style: none; padding: 0; margin: 24px 0 0; position: relative; }
.steps::before { content: ''; position: absolute; left: 14px; top: 0; bottom: 0; width: 2px; background: color-mix(in srgb, var(--fg) 12%, transparent); }
.steps > li { position: relative; display: grid; grid-template-columns: 32px 1fr; gap: 12px; padding: 10px 0 10px 0; }
.steps .dot { width: 14px; height: 14px; border-radius: 50%; background: var(--primary); position: relative; top: 6px; }
.steps .content { padding: 8px 12px; border-radius: 10px; background: color-mix(in srgb, var(--surface) 80%, transparent); border: 1px solid color-mix(in srgb, var(--fg) 10%, transparent); }
.muted { color: var(--muted); }

/* FAQ */
.faq { max-width: 820px; margin: 0 auto; }
.qa { margin: 12px 0; border: 1px solid color-mix(in srgb, var(--fg) 12%, transparent); border-radius: 10px; background: color-mix(in srgb, var(--surface) 80%, transparent); padding: 10px 12px; }
.qa summary { cursor: pointer; font-weight: 700; }
.qa[open] { outline: 1px solid color-mix(in srgb, var(--accent) 40%, transparent); }

/* 푸터/구독 */
.footer { text-align: center; padding: 40px 20px 60px; }
.subscribe { display: grid; grid-template-columns: 1fr auto; gap: 10px; max-width: 420px; margin: 0 auto 14px; }
.subscribe input { padding: 10px 12px; border-radius: 10px; border: 1px solid color-mix(in srgb, var(--fg) 12%, transparent); background: var(--surface); color: var(--fg); }
</style>
