<template>
  <div class="slidev-layout cover">
    <div class="bg-scanlines"></div>
    <div class="bg-vignette"></div>
    <div class="bg-matrix"></div>
    <div class="cover-content">
      <div class="cover-ascii-art">
        <pre style="color: var(--tui-fg-dim); font-size: 0.55rem; line-height: 1.1; text-shadow: none;">&#9484;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9488;
&#9474; slidev-theme-tui v0.1.0      &#9474;
&#9474; Terminal Presentation System  &#9474;
&#9492;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9472;&#9496;</pre>
      </div>
      <div class="cover-title tui-cursor">
        <slot name="default" />
      </div>
      <div class="cover-meta">
        <slot name="info" />
      </div>
      <div class="cover-prompt" style="margin-top: 2rem;">
        <span style="color: var(--tui-accent);">$</span>
        <span style="color: var(--tui-fg);"> slidev present</span>
        <span class="tui-cursor"></span>
      </div>
    </div>
    <div class="tui-statusbar">
      <span class="left">
        <span style="color: var(--tui-warn); font-weight:bold;">-- INSERT --</span>
      </span>
      <span class="right">
        <span>{{ new Date().getFullYear() }}</span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.cover {
  display: flex;
  align-items: center;
  justify-content: center;
}
.cover-content {
  text-align: center;
  z-index: 10;
  position: relative;
}
.cover-title {
  font-size: 2.4rem;
  font-weight: 700;
  color: var(--tui-accent);
  text-shadow: var(--tui-glow-strong);
  margin: 1rem 0 0.5rem;
}
.cover-meta {
  color: var(--tui-fg-dim);
  font-size: 0.9rem;
}
</style>
