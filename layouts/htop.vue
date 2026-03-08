<template>
  <div class="slidev-layout htop">
    <div class="bg-scanlines"></div>
    <!-- htop header -->
    <div class="htop-header">
      <div class="htop-cpu-bars">
        <div v-for="n in 4" :key="n" class="htop-cpu">
          <span class="htop-label">CPU{{ n }}</span>
          <div class="htop-bar">
            <div class="htop-fill" :style="{ width: (20 + n * 15) + '%' }"></div>
          </div>
          <span class="htop-val">{{ 20 + n * 15 }}%</span>
        </div>
        <div class="htop-cpu">
          <span class="htop-label">Mem</span>
          <div class="htop-bar">
            <div class="htop-fill mem" style="width: 42%"></div>
          </div>
          <span class="htop-val">4.2G/16G</span>
        </div>
      </div>
      <div class="htop-stats">
        <div>Tasks: <span class="hl">127</span>, <span class="hl">3</span> running</div>
        <div>Load average: <span class="hl">1.42 1.18 0.94</span></div>
        <div>Uptime: <span class="hl">3 days, 14:22:07</span></div>
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
  display: flex;
  justify-content: space-between;
  padding: 0.6rem 1.2rem;
  background: var(--tui-bg);
  border-bottom: 2px solid var(--tui-border);
  font-size: 0.75rem;
}

.htop-cpu-bars { 
  display: flex; 
  flex-direction: column; 
  gap: 0.3rem; 
  flex: 1; 
}

.htop-cpu { 
  display: flex; 
  align-items: center; 
  gap: 0.6rem; 
}

.htop-label { 
  width: 4rem; 
  color: var(--tui-fg); 
  font-weight: 600;
}

.htop-bar {
  flex: 1; 
  max-width: 220px;
  height: 12px;
  background: var(--tui-bg-alt);
  border: 1px solid var(--tui-border);
  position: relative;
  overflow: hidden;
}

.htop-fill { 
  height: 100%; 
  background: linear-gradient(90deg, var(--tui-accent), rgba(51,255,102,0.7));
  box-shadow: 0 0 8px rgba(51,255,102,0.4);
  transition: width 0.3s ease;
}

.htop-fill.mem { 
  background: linear-gradient(90deg, var(--tui-info), rgba(102,204,255,0.7));
  box-shadow: 0 0 8px rgba(102,204,255,0.4);
}

.htop-val { 
  width: 5.5rem; 
  color: var(--tui-fg); 
  text-align: right; 
  font-weight: 500;
}

.htop-stats { 
  display: flex; 
  flex-direction: column; 
  gap: 0.3rem; 
  font-size: 0.75rem; 
  padding-left: 1.5rem;
}

.htop-stats .hl { 
  color: var(--tui-accent); 
  font-weight: 700;
  text-shadow: 0 0 6px rgba(51,255,102,0.4);
}

.htop-table-header {
  display: flex;
  gap: 1rem;
  padding: 0.3rem 1.2rem;
  background: var(--tui-accent);
  color: var(--tui-bg);
  font-size: 0.75rem;
  font-weight: 700;
  text-shadow: none;
  letter-spacing: 0.02em;
}

.col-pid  { width: 4rem; }
.col-user { width: 6rem; }
.col-cpu  { width: 4rem; }
.col-mem  { width: 4rem; }
.col-cmd  { flex: 1; }

.htop-content { 
  flex: 1; 
  padding: 0.8rem 1.2rem; 
  overflow-y: auto; 
  font-size: 0.82rem; 
}

.htop-footer {
  display: flex;
  gap: 0.3rem;
  background: var(--tui-bg-alt);
  border-top: 1px solid var(--tui-border);
  font-size: 0.7rem;
  padding: 0.3rem 0.5rem;
}

.htop-fn { 
  display: flex; 
  align-items: center; 
  gap: 0.2rem;
  padding: 0.1rem 0.4rem;
  transition: background 0.2s ease;
  cursor: pointer;
}

.htop-fn:hover {
  background: rgba(51,255,102,0.1);
}

.fn-key {
  background: var(--tui-fg);
  color: var(--tui-bg);
  padding: 0.15em 0.4em;
  margin-right: 0.3em;
  font-weight: 700;
  border-radius: 2px;
  box-shadow: 0 1px 2px rgba(0,0,0,0.3);
}
</style>
