<template>
  <div class="term-window" :class="{ 'term-focused': focused }">
    <div class="term-titlebar">
      <span class="dot red"></span>
      <span class="dot yellow"></span>
      <span class="dot green"></span>
      <span class="term-title">{{ title }}</span>
    </div>
    <div class="term-body">
      <div v-if="showPrompt" class="term-prompt-line">
        <span class="term-user">{{ user }}</span>
        <span class="term-at">@</span>
        <span class="term-host">{{ host }}</span>
        <span class="term-sep">:</span>
        <span class="term-path">{{ path }}</span>
        <span class="term-dollar">$</span>
        <span v-if="command" class="term-command"> {{ command }}</span>
        <span v-if="!command" class="tui-cursor"></span>
      </div>
      <slot />
    </div>
  </div>
</template>

<script setup>
defineProps({
  title:      { type: String, default: 'bash' },
  user:       { type: String, default: 'user' },
  host:       { type: String, default: 'localhost' },
  path:       { type: String, default: '~' },
  command:    { type: String, default: '' },
  showPrompt: { type: Boolean, default: true },
  focused:    { type: Boolean, default: true },
})
</script>

<style scoped>
.term-window {
  border: 1px solid var(--tui-border);
  border-radius: 0;
  overflow: hidden;
  box-shadow: 0 0 20px rgba(51,255,102,0.1), inset 0 0 20px rgba(0,0,0,0.4);
  background: var(--tui-bg);
}
.term-focused { box-shadow: 0 0 30px rgba(51,255,102,0.25), inset 0 0 20px rgba(0,0,0,0.4); }
.term-titlebar {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.35rem 0.75rem;
  background: #1c1c1c;
  border-bottom: 1px solid var(--tui-border);
}
.dot { width: 10px; height: 10px; border-radius: 50%; }
.dot.red    { background: #ff5f57; }
.dot.yellow { background: #febc2e; }
.dot.green  { background: #28c840; }
.term-title {
  flex: 1;
  text-align: center;
  font-size: 0.72rem;
  color: #666;
}
.term-body { padding: 0.8rem 1rem; }
.term-prompt-line { display: flex; align-items: center; flex-wrap: wrap; margin-bottom: 0.3rem; }
.term-user   { color: #33ff66; font-weight: 700; }
.term-at     { color: #ffffff; }
.term-host   { color: #33ff66; font-weight: 700; }
.term-sep    { color: #ffffff; }
.term-path   { color: #66ccff; font-weight: 700; }
.term-dollar { color: #ffffff; margin: 0 0.2em; }
.term-command { color: var(--tui-fg); }
</style>
