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
.htop { display: flex; flex-direction: column; }
.htop-header {
  display: flex;
  justify-content: space-between;
  padding: 0.4rem 1rem;
  background: var(--tui-bg);
  border-bottom: 1px solid var(--tui-border);
  font-size: 0.72rem;
}
.htop-cpu-bars { display: flex; flex-direction: column; gap: 0.2rem; flex: 1; }
.htop-cpu { display: flex; align-items: center; gap: 0.4rem; }
.htop-label { width: 3.5rem; color: var(--tui-fg); }
.htop-bar {
  flex: 1; max-width: 200px;
  height: 10px;
  background: var(--tui-bg-alt);
  border: 1px solid var(--tui-border);
}
.htop-fill { height: 100%; background: var(--tui-accent); }
.htop-fill.mem { background: var(--tui-info); }
.htop-val { width: 5rem; color: var(--tui-fg-dim); text-align: right; }
.htop-stats { display: flex; flex-direction: column; gap: 0.2rem; font-size: 0.72rem; }
.htop-stats .hl { color: var(--tui-accent); }
.htop-table-header {
  display: flex;
  gap: 1rem;
  padding: 0.2rem 1rem;
  background: var(--tui-accent);
  color: var(--tui-bg);
  font-size: 0.72rem;
  font-weight: 700;
}
.col-pid  { width: 4rem; }
.col-user { width: 6rem; }
.col-cpu  { width: 4rem; }
.col-mem  { width: 4rem; }
.col-cmd  { flex: 1; }
.htop-content { flex: 1; padding: 0.5rem 1rem; overflow-y: auto; font-size: 0.8rem; }
.htop-footer {
  display: flex;
  background: var(--tui-bg-alt);
  border-top: 1px solid var(--tui-border);
  font-size: 0.7rem;
}
.htop-fn { display: flex; align-items: center; }
.fn-key {
  background: var(--tui-fg);
  color: var(--tui-bg);
  padding: 0.1em 0.3em;
  margin-right: 0.2em;
  font-weight: 700;
}
</style>
