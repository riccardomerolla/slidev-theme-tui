<template>
  <div class="slidev-layout gemini layout-gemini">
    <div class="gemini-bg-gradient"></div>
    <div class="bg-scanlines"></div>
    <div class="bg-vignette"></div>
    <!-- Header -->
    <div class="gemini-header">
      <span class="gemini-logo">&#9670; Gemini CLI</span>
      <span class="gemini-model-badge">gemini-2.5-pro</span>
      <span style="flex:1"></span>
      <span style="font-size:0.65rem; color: rgba(226,232,240,0.4);">PTY Mode &bull; Context: 128k</span>
    </div>
    <!-- Content -->
    <div class="gemini-body">
      <slot />
    </div>
    <!-- Status bar -->
    <div class="gemini-statusbar">
      <span class="indicator">
        <span class="gemini-dot"></span>
        Ready
      </span>
      <span>{{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}</span>
      <span>&#9650; 0 &#9660; 0 tokens</span>
    </div>
  </div>
</template>

<style scoped>
.gemini {
  display: flex;
  flex-direction: column;
  background: #0a0d16;
  color: #e2e8f0;
  position: relative;
}
.gemini-body {
  flex: 1;
  padding: 2.5rem 3rem;
  overflow-y: auto;
  position: relative;
  z-index: 1;
}
</style>
