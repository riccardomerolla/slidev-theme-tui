<template>
  <div class="slidev-layout vim">
    <div class="bg-scanlines"></div>
    <div class="bg-ascii"></div>
    <!-- Vim top bar -->
    <div class="vim-tabline">
      <span class="vim-tab active">presentation.md</span>
      <span class="vim-tab">README.md</span>
    </div>
    <!-- Content area -->
    <div class="vim-editor">
      <div class="vim-gutter">
        <span v-for="n in 20" :key="n" class="vim-lnum">{{ n }}</span>
      </div>
      <div class="vim-content">
        <slot />
      </div>
    </div>
    <!-- Vim status line -->
    <div class="vim-statusline">
      <span class="vim-mode">NORMAL</span>
      <span class="vim-file">presentation.md</span>
      <span class="vim-spacer"></span>
      <span class="vim-pos">{{ $slidev.nav.currentPage }}:1</span>
      <span class="vim-pct">{{ Math.round($slidev.nav.currentPage/$slidev.nav.total*100) }}%</span>
    </div>
    <!-- Vim command line -->
    <div class="vim-cmdline">
      <span class="vim-cmd-cursor">&#8203;</span>
    </div>
  </div>
</template>

<style scoped>
.vim { display: flex; flex-direction: column; }
.vim-tabline {
  display: flex;
  background: var(--tui-bg-alt);
  border-bottom: 1px solid var(--tui-border);
  font-size: 0.75rem;
}
.vim-tab {
  padding: 0.2em 1em;
  color: var(--tui-fg-dim);
  border-right: 1px solid var(--tui-border);
  cursor: pointer;
}
.vim-tab.active {
  background: var(--tui-bg);
  color: var(--tui-fg);
  border-bottom: 2px solid var(--tui-accent);
}
.vim-editor {
  display: flex;
  flex: 1;
  overflow: hidden;
}
.vim-gutter {
  display: flex;
  flex-direction: column;
  padding: 0.5rem 0.5rem;
  background: var(--tui-bg);
  border-right: 1px solid var(--tui-border);
  min-width: 2.5rem;
  text-align: right;
}
.vim-lnum {
  font-size: 0.7rem;
  color: var(--tui-fg-muted);
  line-height: 1.6;
}
.vim-content {
  flex: 1;
  padding: 0.8rem 1.5rem;
  overflow-y: auto;
}
.vim-statusline {
  display: flex;
  align-items: center;
  gap: 1rem;
  height: 1.4rem;
  background: var(--tui-fg);
  color: var(--tui-bg);
  padding: 0 0.5rem;
  font-size: 0.72rem;
  font-weight: 700;
}
.vim-mode { background: var(--tui-bg); color: var(--tui-accent); padding: 0 0.4em; text-shadow: none; }
.vim-spacer { flex: 1; }
.vim-cmdline {
  height: 1.3rem;
  background: var(--tui-bg);
  padding: 0 0.5rem;
  font-size: 0.75rem;
  color: var(--tui-fg);
  display: flex;
  align-items: center;
}
</style>
