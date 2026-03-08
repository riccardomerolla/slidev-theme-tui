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
  width: 100%;
  height: 100%;
  min-height: 100%;
  background: var(--tui-bg);
  color: var(--tui-fg);
  font-family: var(--tui-font);
}

.vim-tabline {
  flex-shrink: 0;
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
  min-height: 0;
  overflow: hidden;
}

.vim-gutter {
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  padding: 1rem 0.6rem;
  background: var(--tui-bg-alt);
  border-right: 2px solid var(--tui-border);
  min-width: 3.5rem;
  text-align: right;
  user-select: none;
}

.vim-lnum {
  font-size: 0.75rem;
  color: var(--tui-fg-muted);
  line-height: 1.6;
  transition: color 0.2s ease;
  font-weight: 500;
}

.vim-lnum:hover {
  color: var(--tui-accent);
  text-shadow: 0 0 4px rgba(51,255,102,0.3);
}

.vim-content {
  flex: 1;
  min-height: 0;
  padding: 1.5rem 2.5rem 2rem;
  overflow-y: auto;
  line-height: 1.6;
  font-size: 0.95rem;
}

.vim-content :deep(h1),
.vim-content :deep(h2),
.vim-content :deep(h3) {
  color: var(--tui-accent);
  text-shadow: 0 0 10px rgba(51,255,102,0.3);
  margin: 1.5rem 0 1rem 0;
  font-weight: 700;
}

.vim-content :deep(h1) {
  font-size: 1.8rem;
}

.vim-content :deep(h2) {
  font-size: 1.4rem;
}

.vim-content :deep(h3) {
  font-size: 1.1rem;
}

.vim-content :deep(p) {
  margin: 0.8rem 0;
  color: var(--tui-fg);
  font-size: 0.95rem;
}

.vim-content :deep(code) {
  background: rgba(0, 0, 0, 0.3);
  color: #00ff99;
  padding: 0.2em 0.4em;
  border-radius: 2px;
  font-family: 'JetBrains Mono', 'Fira Code', monospace;
  border: 1px solid rgba(51,255,102,0.2);
  text-shadow: 0 0 3px rgba(51,255,102,0.2);
}

.vim-content :deep(pre) {
  background: rgba(0, 0, 0, 0.4);
  color: #00ff99;
  padding: 1rem;
  border-left: 3px solid var(--tui-accent);
  border-radius: 2px;
  overflow-x: auto;
  margin: 1rem 0;
  box-shadow: inset 0 0 15px rgba(0,0,0,0.5), 0 0 8px rgba(51,255,102,0.1);
}

.vim-content :deep(pre code) {
  background: none;
  border: none;
  padding: 0;
  color: inherit;
  text-shadow: none;
}

.vim-statusline {
  flex-shrink: 0;
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
  z-index: 50;
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
