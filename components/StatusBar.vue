<template>
  <div class="tui-statusbar" :class="variant">
    <span class="left">
      <span v-if="mode" class="mode-badge">{{ mode }}</span>
      <span v-if="file">{{ file }}</span>
      <slot name="left" />
    </span>
    <span class="center">
      <slot />
    </span>
    <span class="right">
      <slot name="right" />
      <span v-if="showPage">Ln {{ page }}, Col 1</span>
      <span v-if="encoding">{{ encoding }}</span>
    </span>
  </div>
</template>

<script setup>
defineProps({
  mode:     { type: String, default: '' },
  file:     { type: String, default: '' },
  page:     { type: Number, default: 1 },
  encoding: { type: String, default: 'UTF-8' },
  showPage: { type: Boolean, default: false },
  variant:  { type: String, default: '' },
})
</script>

<style scoped>
.tui-statusbar {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  height: 1.6rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: var(--tui-fg);
  color: var(--tui-bg);
  font-size: 0.72rem;
  font-weight: 700;
  padding: 0 0.8em;
  z-index: 50;
  font-family: var(--tui-font);
}
.tui-statusbar .left  { display: flex; gap: 0.8em; align-items: center; }
.tui-statusbar .right { display: flex; gap: 0.8em; align-items: center; }
.tui-statusbar .center { flex: 1; text-align: center; }
.mode-badge {
  background: var(--tui-bg);
  color: var(--tui-accent);
  padding: 0 0.3em;
  text-shadow: none;
}
.tui-statusbar.gemini {
  background: linear-gradient(90deg, rgba(129,140,248,0.2), rgba(52,211,153,0.15));
  color: rgba(226,232,240,0.7);
  border-top: 1px solid rgba(129,140,248,0.3);
}
</style>
