<template>
  <div class="slidev-layout htop">
    <div class="bg-scanlines" style="opacity: 0.26"></div>
    <div class="htop-shell">
      <div class="spawn-line">
        <span class="spawn-symbol">&gt;</span>
        <span class="spawn-text">spawn --process</span>
        <span class="spawn-agent">Agent_AI</span>
        <span class="spawn-cursor">█</span>
      </div>

      <HtopHeadline :title="htopTitle" />

      <div class="htop-grid">
        <section class="pane pane-left">
          <div class="pane-title">[ PROCESS_DETAILS ]</div>
          <div class="pane-content">
            <slot />
          </div>
        </section>

        <section class="pane pane-right">
          <div class="pane-title">[ TOP_PROCESSES ]</div>

          <div class="meter-block">
            <div class="meter-row" v-for="m in meters" :key="m.label">
              <span class="meter-label">{{ m.label }}</span>
              <div class="meter-bar"><span :style="{ width: m.value }"></span></div>
              <span class="meter-value">{{ m.text }}</span>
            </div>
          </div>

          <div class="table-head">
            <span>PID</span>
            <span>USER</span>
            <span>CPU%</span>
            <span>MEM%</span>
            <span>TIME+</span>
            <span>COMMAND</span>
          </div>

          <div
            class="table-row"
            v-for="proc in processes"
            :key="proc.pid"
            :class="{ active: proc.active }"
          >
            <span>{{ proc.pid }}</span>
            <span>{{ proc.user }}</span>
            <span>{{ proc.cpu }}</span>
            <span>{{ proc.mem }}</span>
            <span>{{ proc.time }}</span>
            <span>{{ proc.cmd }}</span>
          </div>

          <div class="status-strip">[ SYSTEM_STATUS: AI_INTEGRATION ] | CPU: 92% | MEM: 64% | AGENTS: ACTIVE</div>
        </section>
      </div>

      <div class="status-strip shell-bottom">[ SYSTEM_STATUS: AI_INTEGRATION ] | CPU: 92% | MEM: 64% | AGENTS: ACTIVE</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useSlideContext } from '@slidev/client'

const { $slidev } = useSlideContext()

const htopTitle = computed(() => {
  const currentIndex = $slidev.nav.currentPage - 1
  const currentSlide = $slidev.nav.slides?.[currentIndex]
  const frontmatter = currentSlide?.frontmatter ?? {}
  return frontmatter.htopTitle || frontmatter.title || 'Il Livello Successivo: Autonomia con Agent AI'
})

const meters = [
  { label: '1', value: '8%', text: '0.0%' },
  { label: '2', value: '9%', text: '0.0%' },
  { label: '3', value: '11%', text: '0.0%' },
  { label: 'Net', value: '58%', text: '587/7206Kb' },
  { label: 'Swp', value: '7%', text: '407.2K' },
]

const processes = [
  { pid: '1337', user: 'admin', cpu: '28.3', mem: '124.5', time: '4:12.56', cmd: 'Agent_AI', active: true },
  { pid: '995', user: 'root', cpu: '21.4', mem: '85.2', time: '2:45.21', cmd: 'refactor_engine', active: false },
  { pid: '2280', user: 'user', cpu: '15.1', mem: '60.8', time: '1:55.89', cmd: 'Gemini_CLI', active: false },
  { pid: '7771', user: 'admin', cpu: '23.6', mem: '45.9', time: '1:32.10', cmd: 'analysis_bot', active: false },
  { pid: '4490', user: 'root', cpu: '12.8', mem: '32.4', time: '0:58.42', cmd: 'logger', active: false },
]
</script>

<style scoped>
.htop {
  width: 100%;
  height: 100%;
  min-height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  background:
    radial-gradient(circle at 8% 8%, rgba(0, 255, 163, 0.22), transparent 32%),
    radial-gradient(circle at 88% 12%, rgba(0, 212, 255, 0.2), transparent 30%),
    #030606;
}

.htop-shell {
  width: 100%;
  height: 100%;
  min-height: 0;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
  padding: 1rem 1.1rem 0.9rem;
  border: 2px solid #11ffd0;
  border-radius: 8px;
  background: rgba(0, 0, 0, 0.88);
  box-shadow:
    0 0 12px rgba(17, 255, 208, 0.6),
    inset 0 0 22px rgba(3, 190, 156, 0.25);
}

.spawn-line {
  display: flex;
  align-items: center;
  gap: 0.45rem;
  color: #c8d0cc;
  font-size: 0.78rem;
  letter-spacing: 0.01em;
}

.spawn-symbol {
  color: #11ffd0;
  font-weight: 700;
}

.spawn-text {
  color: #9be9c4;
}

.spawn-agent {
  color: #f3f3f3;
  font-weight: 600;
}

.spawn-cursor {
  color: #f0f0f0;
  animation: blink 1.1s step-start infinite;
}

.htop-grid {
  min-height: 0;
  flex: 1;
  display: grid;
  grid-template-columns: 1fr 1.05fr;
  gap: 0.75rem;
}

.pane {
  min-height: 0;
  border: 2px solid #00eaff;
  border-radius: 6px;
  background: rgba(0, 0, 0, 0.8);
  box-shadow: 0 0 12px rgba(0, 234, 255, 0.36), inset 0 0 12px rgba(0, 0, 0, 0.7);
  display: flex;
  flex-direction: column;
}

.pane-title {
  color: #42e8ff;
  text-align: center;
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  padding: 0.28rem 0.65rem;
  border-bottom: 1px solid rgba(0, 234, 255, 0.45);
}

.pane-content {
  flex: 1;
  min-height: 0;
  padding: 0.95rem 1rem;
  overflow-y: auto;
}

.pane-content :deep(p) {
  margin: 0 0 0.8rem;
  color: #e7ece8;
  font-size: clamp(0.92rem, 1.35vw, 1.05rem);
  line-height: 1.35;
  font-weight: 600;
}

.pane-content :deep(strong) {
  color: #54ff74;
  text-shadow: 0 0 8px rgba(84, 255, 116, 0.5);
}

.pane-content :deep(code) {
  background: rgba(0, 0, 0, 0.45);
  border: 1px solid rgba(0, 234, 255, 0.45);
  color: #54ff74;
}

.pane-right {
  padding-bottom: 0.55rem;
}

.meter-block {
  padding: 0.4rem 0.7rem 0.3rem;
  border-bottom: 1px solid rgba(0, 234, 255, 0.36);
}

.meter-row {
  display: grid;
  grid-template-columns: 1.8rem 1fr auto;
  align-items: center;
  gap: 0.45rem;
  font-size: 0.7rem;
  color: #9ce6ff;
  margin-bottom: 0.15rem;
}

.meter-bar {
  height: 0.42rem;
  background: rgba(6, 20, 24, 0.8);
  border: 1px solid rgba(0, 234, 255, 0.28);
}

.meter-bar span {
  display: block;
  height: 100%;
  background: linear-gradient(90deg, #1ee6ff, #52ff74);
  box-shadow: 0 0 6px rgba(82, 255, 116, 0.45);
}

.table-head,
.table-row {
  display: grid;
  grid-template-columns: 3.4rem 3.2rem 2.6rem 2.8rem 3.5rem 1fr;
  gap: 0.4rem;
  padding: 0.12rem 0.7rem;
  font-size: 0.68rem;
  align-items: center;
}

.table-head {
  margin-top: 0.3rem;
  color: #9defff;
  font-weight: 700;
  border-top: 1px solid rgba(0, 234, 255, 0.35);
  border-bottom: 1px solid rgba(0, 234, 255, 0.35);
}

.table-row {
  color: #d8dedb;
  font-weight: 600;
}

.table-row.active {
  background: linear-gradient(90deg, rgba(84, 255, 116, 0.55), rgba(84, 255, 116, 0.12));
  color: #06180b;
  font-weight: 800;
}

.status-strip {
  margin: 0.45rem 0.7rem 0;
  border: 2px solid #00eaff;
  border-radius: 4px;
  color: #5df67c;
  font-size: 0.72rem;
  font-weight: 700;
  letter-spacing: 0.02em;
  padding: 0.24rem 0.55rem;
  box-shadow: inset 0 0 9px rgba(0, 234, 255, 0.2), 0 0 8px rgba(0, 234, 255, 0.25);
}

.shell-bottom {
  margin: 0;
}

@keyframes blink {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}

@media (max-width: 1024px) {
  .htop-grid {
    grid-template-columns: 1fr;
  }

  .table-head,
  .table-row {
    grid-template-columns: 3.2rem 3rem 2.4rem 2.6rem 3.3rem 1fr;
  }
}
</style>
