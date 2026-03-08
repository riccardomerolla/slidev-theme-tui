<template>
  <div class="slidev-layout default">
    <!-- Background layers -->
    <div class="bg-scanlines"></div>
    <div class="bg-vignette"></div>
    <div class="bg-noise"></div>
    <!-- Top bar -->
    <div class="tui-topbar">
      <span class="left">
        <span class="dot-indicator" style="color: var(--tui-warn)">&#9632;</span>
        <span class="dot-indicator" style="color: var(--tui-error)">&#9632;</span>
        <span class="dot-indicator" style="color: var(--tui-accent)">&#9632;</span>
        <span class="separator">&#9474;</span>
        <span class="title">slidev-theme-tui</span>
      </span>
      <span class="right">
        <span class="page-indicator">{{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}</span>
      </span>
    </div>
    <!-- Main content -->
    <div class="tui-content">
      <slot />
    </div>
    <!-- Status bar -->
    <div class="tui-statusbar">
      <span class="left">
        <span class="mode-badge">NORMAL</span>
        <span>slides/presentation.md</span>
      </span>
      <span class="right">
        <span>Ln {{ $slidev.nav.currentPage }}, Col 1</span>
        <span>UTF-8</span>
        <span>TUI</span>
      </span>
    </div>
  </div>
</template>

<script setup>
import { useNav } from '@slidev/client'
const { currentPage, total } = useNav()
</script>

<style scoped>
.default {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 100%;
  background: var(--tui-bg);
  color: var(--tui-fg);
  font-family: var(--tui-font);
  display: flex;
  flex-direction: column;
}

.tui-topbar {
  flex-shrink: 0;
  position: relative;
  z-index: 50;
}

.tui-topbar .dot-indicator {
  transition: all 0.2s ease;
}

.tui-topbar .separator {
  margin: 0 0.5rem;
  color: var(--tui-border);
}

.tui-topbar .title {
  font-weight: 600;
  letter-spacing: 0.02em;
}

.tui-topbar .page-indicator {
  font-weight: 600;
  color: var(--tui-accent);
  text-shadow: 0 0 8px rgba(51,255,102,0.4);
}

.tui-statusbar {
  flex-shrink: 0;
  position: relative;
  z-index: 50;
}

.tui-statusbar .mode-badge {
  animation: pulse 2s ease-in-out infinite;
}

.tui-content {
  flex: 1;
  min-height: 0;
  padding: 2rem 3.5rem;
  overflow-y: auto;
  max-width: 100%;
  margin: 0 auto;
  width: 100%;
}

.tui-content :deep(h1) {
  color: var(--tui-accent);
  font-size: 2.2rem;
  font-weight: 700;
  margin: 0 0 1.2rem;
  text-shadow: 0 0 12px rgba(51, 255, 102, 0.5);
  letter-spacing: 0.02em;
}

.tui-content :deep(h2) {
  color: var(--tui-accent);
  font-size: 1.6rem;
  font-weight: 700;
  margin: 1.5rem 0 0.8rem;
  text-shadow: 0 0 8px rgba(51, 255, 102, 0.4);
}

.tui-content :deep(h3) {
  color: #00ff99;
  font-size: 1.2rem;
  margin: 1rem 0 0.6rem;
}

.tui-content :deep(p) {
  color: var(--tui-fg);
  font-size: 1rem;
  line-height: 1.6;
  margin: 0.6rem 0;
}

.tui-content :deep(ul),
.tui-content :deep(ol) {
  margin: 0.8rem 0;
  padding-left: 2em;
}

.tui-content :deep(li) {
  color: var(--tui-fg);
  font-size: 1rem;
  line-height: 1.5;
  margin: 0.4rem 0;
}

.tui-content :deep(code) {
  font-family: var(--tui-font);
  background: rgba(51, 255, 102, 0.08);
  color: #00ff99;
  padding: 0.2em 0.5em;
  border-radius: 3px;
  border: 1px solid rgba(51, 255, 102, 0.2);
  font-size: 0.9em;
  text-shadow: 0 0 4px rgba(51, 255, 102, 0.3);
}

.tui-content :deep(pre) {
  background: rgba(20, 40, 30, 0.85);
  border: 1px solid rgba(51, 255, 102, 0.25);
  border-left: 3px solid var(--tui-accent);
  padding: 1.2em 1.5em;
  border-radius: 4px;
  overflow-x: auto;
  margin: 1rem 0;
  box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.4), 0 0 16px rgba(51, 255, 102, 0.1);
  line-height: 1.5;
}

.tui-content :deep(pre code) {
  background: transparent;
  border: none;
  color: var(--tui-fg);
  padding: 0;
  text-shadow: none;
}

.tui-content :deep(blockquote) {
  border-left: 3px solid var(--tui-warn);
  margin: 1rem 0;
  padding: 0.8em 1.2em;
  background: rgba(255, 183, 0, 0.05);
  color: rgba(255, 183, 0, 0.9);
  font-style: italic;
  font-size: 0.95rem;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.8; }
}
</style>
