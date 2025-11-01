<template>
  <div :class="['app', isDark ? 'theme-dark' : 'theme-light']">
    <header class="nav">
      <div class="brand" @click="scrollTo('#hero')">
        <span>🌕 한가위 한 페이지</span>
      </div>
      <nav class="links">
        <a href="#about">소개</a>
        <a href="#foods">전통 음식</a>
        <a href="#games">전통 놀이</a>
        <a href="#gallery">갤러리</a>
      </nav>
      <button class="toggle" @click="toggleTheme">
        <span v-if="isDark">☀️ 밝게</span>
        <span v-else>🌙 어둡게</span>
      </button>
    </header>

    <section id="hero" class="hero">
      <div class="hero-inner">
        <h1>한가위, 보름달처럼 가득 찬 <em>마음</em></h1>
        <p class="subtitle">
          가족과 이웃에게 온기를 전하는 날, <strong>추석</strong>의 이야기를 담았습니다.
        </p>
        <Countdown target="2025-09-07T00:00:00" label="올해 추석까지" />
      </div>
    </section>

    <footer class="footer">
      <p>© {{ year }} 한가위 한 페이지 · 보름달처럼 넉넉한 하루 되세요.</p>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted, defineComponent } from 'vue'

const isDark = ref<boolean>(
    window.matchMedia?.('(prefers-color-scheme: dark)').matches ?? false
)
const toggleTheme = () => (isDark.value = !isDark.value)

const scrollTo = (sel: string) =>
    document.querySelector(sel)?.scrollIntoView({ behavior: 'smooth' })

const year = new Date().getFullYear()

/* 카운트다운 컴포넌트 */
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

    // ✅ id 변수 타입 지정 및 해제 처리 (빌드 오류 해결)
    let intervalId: number | undefined

    onMounted(() => {
      tick()
      intervalId = window.setInterval(tick, 1000)
    })

    onUnmounted(() => {
      if (intervalId !== undefined) window.clearInterval(intervalId)
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
.app {
  background: var(--bg, #0b1020);
  color: var(--fg, #e6edf6);
  min-height: 100vh;
  text-align: center;
  transition: background 0.4s;
}

.theme-light {
  --bg: #f8fafc;
  --fg: #0b1020;
}

.nav {
  display: flex;
  justify-content: space-between;
  padding: 12px 20px;
  background: rgba(0, 0, 0, 0.2);
}

.links a {
  margin: 0 8px;
  text-decoration: none;
  color: inherit;
}

.toggle {
  border: none;
  background: transparent;
  cursor: pointer;
  font-size: 18px;
}

.hero {
  padding: 80px 20px;
}

.subtitle {
  color: #b6c2d6;
  margin-bottom: 16px;
}

.countdown {
  display: inline-grid;
  gap: 4px;
  background: rgba(255, 255, 255, 0.1);
  padding: 10px 16px;
  border-radius: 8px;
}

.footer {
  margin-top: 40px;
  color: #b6c2d6;
  padding-bottom: 30px;
}
</style>
