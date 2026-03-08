<template>
  <div class="slidev-layout default">
    <!-- Background layers -->
    <div class="bg-scanlines"></div>
    <div class="bg-vignette"></div>
    <!-- Top bar -->
    <div class="tui-topbar">
      <span class="left">
        <span style="color: var(--tui-warn)">&#9632;</span>
        <span style="color: var(--tui-error)">&#9632;</span>
        <span style="color: var(--tui-accent)">&#9632;</span>
        &nbsp; slidev-theme-tui
      </span>
      <span class="right">{{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}</span>
    </div>
    <!-- Main content -->
    <div class="tui-content" style="padding-top: 3rem; padding-bottom: 3rem;">
      <slot />
    </div>
    <!-- Status bar -->
    <div class="tui-statusbar">
      <span class="left">
        <span>NORMAL</span>
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
