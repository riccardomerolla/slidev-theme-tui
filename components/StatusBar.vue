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
  position: fixed;
  bottom: 0; 
  left: 0; 
  right: 0;
  width: 100%;
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: linear-gradient(180deg, var(--tui-fg) 0%, rgba(51,255,102,0.95) 100%);
  color: var(--tui-bg);
  font-size: 0.8rem;
  font-weight: 700;
  padding: 0 1.2rem;
  z-index: 9999;
  font-family: var(--tui-font);
  border-top: 1px solid rgba(255,255,255,0.1);
  box-shadow: 0 -2px 10px rgba(51,255,102,0.3);
}

.tui-statusbar .left  { 
  display: flex; 
  gap: 1rem; 
  align-items: center; 
}

.tui-statusbar .right { 
  display: flex; 
  gap: 1rem; 
  align-items: center; 
}

.tui-statusbar .center { 
  flex: 1; 
  text-align: center;
  font-weight: 600;
}

.mode-badge {
  background: var(--tui-bg);
  color: var(--tui-accent);
  padding: 0.2em 0.7em;
  text-shadow: none;
  border-radius: 3px;
  font-weight: 700;
  letter-spacing: 0.02em;
  border: 1px solid rgba(51,255,102,0.3);
}

.tui-statusbar.gemini {
  background: linear-gradient(
    90deg, 
    rgba(129,140,248,0.25), 
    rgba(52,211,153,0.2)
  );
  color: rgba(226,232,240,0.85);
  border-top: 1px solid rgba(129,140,248,0.4);
  backdrop-filter: blur(4px);
}
</style>
