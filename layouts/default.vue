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
    <div class="tui-content" style="padding-top: 3.5rem; padding-bottom: 3.5rem;">
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

.tui-statusbar .mode-badge {
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.8; }
}
</style>
