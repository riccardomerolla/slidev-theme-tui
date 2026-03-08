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
  </div>
</template>

<style scoped>
.vim { 
  display: flex; 
  flex-direction: column; 
}

.vim-tabline {
  display: flex;
  background: var(--tui-bg-alt);
  border-bottom: 1px solid var(--tui-border);
  font-size: 0.75rem;
}

.vim-tab {
  padding: 0.3em 1.2em;
  color: var(--tui-fg-dim);
  border-right: 1px solid var(--tui-border);
  cursor: pointer;
  transition: all 0.2s ease;
  position: relative;
}

.vim-tab:hover {
  color: var(--tui-fg);
  background: rgba(51,255,102,0.05);
}

.vim-tab.active {
  background: var(--tui-bg);
  color: var(--tui-fg);
  border-bottom: 2px solid var(--tui-accent);
  box-shadow: 0 0 8px rgba(51,255,102,0.2);
}

.vim-editor {
  display: flex;
  flex: 1;
  overflow: hidden;
}

.vim-gutter {
  display: flex;
  flex-direction: column;
  padding: 0.8rem 0.6rem;
  background: var(--tui-bg-alt);
  border-right: 2px solid var(--tui-border);
  min-width: 3rem;
  text-align: right;
  user-select: none;
}

.vim-lnum {
  font-size: 0.72rem;
  color: var(--tui-fg-muted);
  line-height: 1.6;
  transition: color 0.2s ease;
}

.vim-lnum:hover {
  color: var(--tui-fg-dim);
}

.vim-content {
  flex: 1;
  padding: 1rem 2rem 3rem 2rem;
  overflow-y: auto;
  line-height: 1.6;
}

.vim-statusline {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  width: 100%;
  display: flex;
  align-items: center;
  gap: 1rem;
  height: 2rem;
  background: linear-gradient(180deg, var(--tui-fg) 0%, rgba(51,255,102,0.95) 100%);
  color: var(--tui-bg);
  padding: 0 1.2rem;
  font-size: 0.8rem;
  font-weight: 700;
  border-top: 1px solid rgba(255,255,255,0.1);
  box-shadow: 0 -2px 10px rgba(51,255,102,0.3);
  z-index: 9999;
}

.vim-mode { 
  background: var(--tui-bg); 
  color: var(--tui-accent); 
  padding: 0.2em 0.7em; 
  text-shadow: none;
  border-radius: 3px;
  font-weight: 700;
  border: 1px solid rgba(51,255,102,0.3);
}

.vim-spacer { flex: 1; }

.vim-cmdline {
  display: none;
}
</style>
