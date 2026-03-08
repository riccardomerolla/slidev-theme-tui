<template>
  <div class="slidev-layout htop">
    <div class="bg-scanlines" style="opacity: 0.3;"></div>
    <!-- htop header -->
    <div class="htop-header">
      <div class="htop-left">
        <div class="htop-row" v-for="n in 4" :key="'cpu' + n">
          <span class="htop-label">{{ n }}</span>
          <div class="htop-bar-wrapper">
            <div class="htop-bar-segment user" :style="{ width: (8 + n * 6) + '%' }"></div>
            <div class="htop-bar-segment system" :style="{ width: (4 + n * 2) + '%' }"></div>
            <div class="htop-bar-segment nice" :style="{ width: (2 + n) + '%' }"></div>
          </div>
          <span class="htop-val">{{ 20 + n * 15 }}%</span>
        </div>
        <div class="htop-row">
          <span class="htop-label mem-label">Mem</span>
          <div class="htop-bar-wrapper">
            <div class="htop-bar-segment mem-used" style="width: 26%"></div>
            <div class="htop-bar-segment mem-buffers" style="width: 8%"></div>
            <div class="htop-bar-segment mem-cache" style="width: 8%"></div>
          </div>
          <span class="htop-val">4.2G/16G</span>
        </div>
        <div class="htop-row">
          <span class="htop-label mem-label">Swp</span>
          <div class="htop-bar-wrapper">
            <div class="htop-bar-segment swap-used" style="width: 5%"></div>
          </div>
          <span class="htop-val">512M/8.0G</span>
        </div>
      </div>
      <div class="htop-right">
        <div class="htop-stat">Tasks: <span class="hl">127</span>, <span class="thr-val">47</span> thr; <span class="run-val">3</span> running</div>
        <div class="htop-stat">Load average: <span class="hl">1.42</span> <span class="hl">1.18</span> <span class="hl">0.94</span></div>
        <div class="htop-stat">Uptime: <span class="hl">3 days, 14:22:07</span></div>
      </div>
    </div>
    <!-- Process table -->
    <div class="htop-table-header">
      <span class="col-pid">PID</span>
      <span class="col-user">USER</span>
      <span class="col-cpu">CPU%</span>
      <span class="col-mem">MEM%</span>
      <span class="col-cmd">COMMAND</span>
    </div>
    <div class="htop-content">
      <slot />
    </div>
    <!-- htop footer -->
    <div class="htop-footer">
      <span class="htop-fn"><span class="fn-key">F1</span>Help</span>
      <span class="htop-fn"><span class="fn-key">F2</span>Setup</span>
      <span class="htop-fn"><span class="fn-key">F3</span>Search</span>
      <span class="htop-fn"><span class="fn-key">F4</span>Filter</span>
      <span class="htop-fn"><span class="fn-key">F5</span>Tree</span>
      <span class="htop-fn"><span class="fn-key">F6</span>SortBy</span>
      <span class="htop-fn"><span class="fn-key">F9</span>Kill</span>
      <span class="htop-fn"><span class="fn-key">F10</span>Quit</span>
    </div>
  </div>
</template>

<style scoped>
.htop { 
  display: flex; 
  flex-direction: column; 
}

.htop-header {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 1.5rem;
  padding: 0.5rem 1.2rem;
  background: rgba(0, 0, 0, 0.8);
  border-bottom: 1px solid rgba(51, 255, 102, 0.3);
  font-size: 0.7rem;
  font-family: 'JetBrains Mono', 'Fira Code', monospace;
}

.htop-left {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
}

.htop-right {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
  justify-content: center;
}

.htop-row {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  line-height: 1.2;
}

.htop-label {
  color: var(--tui-accent);
  font-weight: 700;
  width: 1.2rem;
  text-align: right;
}

.htop-label.mem-label {
  width: 1.8rem;
}

.htop-bar-wrapper {
  flex: 1;
  max-width: 280px;
  height: 10px;
  background: rgba(0, 0, 0, 0.5);
  border: 1px solid rgba(51, 255, 102, 0.2);
  display: flex;
  overflow: hidden;
}

.htop-bar-segment {
  height: 100%;
  transition: width 0.3s ease;
}

/* CPU segments - authentic htop colors */
.htop-bar-segment.user {
  background: #00aa00;
}

.htop-bar-segment.system {
  background: #cc0000;
}

.htop-bar-segment.nice {
  background: #0000aa;
}

/* Memory segments */
.htop-bar-segment.mem-used {
  background: #00aa00;
}

.htop-bar-segment.mem-buffers {
  background: #0000aa;
}

.htop-bar-segment.mem-cache {
  background: #aaaa00;
}

/* Swap */
.htop-bar-segment.swap-used {
  background: #cc0000;
}

.htop-val {
  color: rgba(255, 255, 255, 0.8);
  font-size: 0.7rem;
  min-width: 5rem;
  text-align: right;
}

.htop-stat {
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.3;
  font-size: 0.7rem;
}

.htop-stat .hl {
  color: var(--tui-accent);
  font-weight: 700;
}

.htop-stat .thr-val {
  color: #00aa00;
  font-weight: 600;
}

.htop-stat .run-val {
  color: #00aa00;
  font-weight: 700;
}

.htop-table-header {
  display: flex;
  gap: 1rem;
  padding: 0.4rem 1.2rem;
  background: rgba(0, 0, 0, 0.9);
  color: var(--tui-accent);
  font-size: 0.7rem;
  font-weight: 700;
  border-bottom: 1px solid rgba(51, 255, 102, 0.3);
}

.col-pid  { width: 4rem; }
.col-user { width: 6rem; }
.col-cpu  { width: 4rem; }
.col-mem  { width: 4rem; }
.col-cmd  { flex: 1; }

.htop-content { 
  flex: 1; 
  padding: 2rem 3rem 5rem 3rem; 
  overflow-y: auto; 
  font-size: 1rem;
  line-height: 1.6;
}

.htop-footer {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
  background: rgba(0, 0, 0, 0.95);
  color: rgba(255, 255, 255, 0.9);
  border-top: 1px solid rgba(51, 255, 102, 0.3);
  font-size: 0.7rem;
  padding: 0.35rem 1rem;
  z-index: 9999;
  font-family: 'JetBrains Mono', 'Fira Code', monospace;
}

.htop-fn {
  display: flex;
  align-items: center;
  gap: 0.2rem;
}

.fn-key {
  background: rgba(0, 0, 0, 0.8);
  color: var(--tui-accent);
  padding: 0.15em 0.4em;
  font-weight: 700;
  border: 1px solid rgba(51, 255, 102, 0.3);
}
</style>
