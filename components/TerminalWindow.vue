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
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(51,255,102,0.15), 
              inset 0 0 20px rgba(0,0,0,0.4);
  background: var(--tui-bg);
  transition: all 0.3s ease;
}

.term-focused { 
  box-shadow: 0 6px 30px rgba(51,255,102,0.3), 
              inset 0 0 20px rgba(0,0,0,0.4); 
  transform: translateY(-2px);
}

.term-titlebar {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.4rem 0.85rem;
  background: linear-gradient(180deg, #1f1f1f 0%, #1a1a1a 100%);
  border-bottom: 1px solid var(--tui-border);
}

.dot { 
  width: 12px; 
  height: 12px; 
  border-radius: 50%; 
  transition: all 0.2s ease;
  cursor: pointer;
}

.dot:hover {
  transform: scale(1.15);
  filter: brightness(1.2);
}

.dot.red    { background: #ff5f57; box-shadow: 0 0 4px rgba(255,95,87,0.6); }
.dot.yellow { background: #febc2e; box-shadow: 0 0 4px rgba(254,188,46,0.6); }
.dot.green  { background: #28c840; box-shadow: 0 0 4px rgba(40,200,64,0.6); }

.term-title {
  flex: 1;
  text-align: center;
  font-size: 0.75rem;
  color: #888;
  font-weight: 500;
}

.term-body { 
  padding: 1rem 1.2rem; 
  min-height: 3rem;
}

.term-prompt-line { 
  display: flex; 
  align-items: center; 
  flex-wrap: wrap; 
  margin-bottom: 0.4rem; 
}

.term-user   { 
  color: #33ff66; 
  font-weight: 700; 
  text-shadow: 0 0 6px rgba(51,255,102,0.4);
}

.term-at     { color: #ffffff; margin: 0 0.1em; }

.term-host   { 
  color: #33ff66; 
  font-weight: 700;
  text-shadow: 0 0 6px rgba(51,255,102,0.4);
}

.term-sep    { color: #ffffff; margin: 0 0.1em; }

.term-path   { 
  color: #66ccff; 
  font-weight: 700;
  text-shadow: 0 0 6px rgba(102,204,255,0.4);
}

.term-dollar { 
  color: #ffffff; 
  margin: 0 0.3em; 
  font-weight: 700;
}

.term-command { 
  color: var(--tui-fg); 
  text-shadow: var(--tui-glow);
}
</style>
