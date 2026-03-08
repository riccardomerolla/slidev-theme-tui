<template>
  <div class="slidev-layout terminal">
    <div class="bg-scanlines"></div>
    <div class="bg-vignette"></div>
    <!-- Terminal window -->
    <div class="term-window">
      <div class="term-titlebar">
        <span class="dot red"></span>
        <span class="dot yellow"></span>
        <span class="dot green"></span>
        <span class="term-title">{{ $slidev.configs.title || 'terminal' }} -- bash -- 120x40</span>
      </div>
      <div class="term-body">
        <div class="term-prompt">
          <span class="term-user">user@tui</span><span class="term-sep">:</span><span class="term-path">~</span><span class="term-dollar">$</span>
        </div>
        <slot />
      </div>
    </div>
    <div class="tui-statusbar">
      <span class="left"><span>bash</span><span>PID: 1337</span></span>
      <span class="right"><span>{{ $slidev.nav.currentPage }}/{{ $slidev.nav.total }}</span></span>
    </div>
  </div>
</template>

<style scoped>
.terminal { 
  display: flex; 
  align-items: center; 
  justify-content: center; 
  position: relative;
}

.term-window {
  width: 90%; 
  max-height: 85%;
  border: 1px solid var(--tui-border);
  border-radius: 8px;
  box-shadow: 0 4px 30px rgba(51,255,102,0.2), 
              inset 0 0 30px rgba(0,0,0,0.5);
  overflow: hidden;
  animation: slideInUp 0.5s ease-out;
}

@keyframes slideInUp {
  from { 
    opacity: 0; 
    transform: translateY(20px); 
  }
  to { 
    opacity: 1; 
    transform: translateY(0); 
  }
}

.term-titlebar {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.45rem 0.9rem;
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
  margin-left: 0.5rem; 
  font-size: 0.75rem; 
  color: #888; 
  flex: 1; 
  text-align: center;
  font-weight: 500;
}

.term-body { 
  padding: 1.2rem 1.5rem; 
  min-height: 65%; 
}

.term-prompt { 
  margin-bottom: 0.6rem; 
  display: flex;
  align-items: center;
}

.term-user   { 
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
  margin-left: 0.1em; 
  margin-right: 0.5em;
  font-weight: 700;
}
</style>
