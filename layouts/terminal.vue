<template>
  <div class="slidev-layout terminal">
    <div class="bg-scanlines"></div>
    <div class="bg-vignette"></div>
    <div class="bg-noise"></div>
    
    <!-- Terminal window -->
    <div class="terminal-container">
      <div class="term-window">
        <div class="term-titlebar">
          <div class="dots-container">
            <span class="dot red"></span>
            <span class="dot yellow"></span>
            <span class="dot green"></span>
          </div>
          <span class="term-title">{{ $slidev.configs.title || 'terminal' }} -- bash -- 120x40</span>
          <div class="dots-spacer"></div>
        </div>
        <div class="term-body">
          <div class="term-prompt">
            <span class="term-user">user</span><span class="term-at">@</span><span class="term-host">tui</span><span class="term-sep">:</span><span class="term-path">~</span><span class="term-dollar">$</span>
          </div>
          <div class="term-content">
            <slot />
          </div>
        </div>
      </div>
    </div>
    
    <!-- Status bar -->
    <div class="terminal-statusbar">
      <span class="left">
        <span class="status-item shell">bash</span>
        <span class="separator">│</span>
        <span class="status-item">PID: 1337</span>
      </span>
      <span class="center"></span>
      <span class="right">
        <span class="status-item page">{{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}</span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.terminal { 
  display: flex; 
  align-items: center; 
  justify-content: center; 
  position: relative;
  padding: 2rem;
}

.terminal-container {
  width: 100%;
  max-width: 1100px;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.term-window {
  width: 100%;
  max-height: 75vh;
  border: 1px solid rgba(51,255,102,0.3);
  border-radius: 10px;
  box-shadow: 0 8px 40px rgba(51,255,102,0.25), 
              0 0 60px rgba(51,255,102,0.1),
              inset 0 0 40px rgba(0,0,0,0.6);
  overflow: hidden;
  animation: terminalFadeIn 0.6s ease-out;
  background: rgba(13,17,23,0.95);
}

@keyframes terminalFadeIn {
  from { 
    opacity: 0; 
    transform: translateY(30px) scale(0.98); 
  }
  to { 
    opacity: 1; 
    transform: translateY(0) scale(1); 
  }
}

.term-titlebar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.6rem 1rem;
  background: linear-gradient(180deg, #2a2a2a 0%, #1f1f1f 50%, #1a1a1a 100%);
  border-bottom: 1px solid rgba(51,255,102,0.2);
  box-shadow: 0 1px 3px rgba(0,0,0,0.5);
}

.dots-container {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}

.dot { 
  width: 13px; 
  height: 13px; 
  border-radius: 50%; 
  transition: all 0.2s ease;
  cursor: pointer;
  position: relative;
}

.dot::before {
  content: '';
  position: absolute;
  inset: 2px;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(255,255,255,0.4) 0%, transparent 50%);
}

.dot:hover {
  transform: scale(1.15);
  filter: brightness(1.3);
}

.dot.red    { 
  background: #ff5f57; 
  box-shadow: 0 0 6px rgba(255,95,87,0.7),
              inset 0 1px 2px rgba(255,255,255,0.3);
}
.dot.yellow { 
  background: #febc2e; 
  box-shadow: 0 0 6px rgba(254,188,46,0.7),
              inset 0 1px 2px rgba(255,255,255,0.3);
}
.dot.green  { 
  background: #28c840; 
  box-shadow: 0 0 6px rgba(40,200,64,0.7),
              inset 0 1px 2px rgba(255,255,255,0.3);
}

.term-title { 
  font-size: 0.78rem; 
  color: #999; 
  font-weight: 500;
  letter-spacing: 0.01em;
  text-align: center;
  flex: 1;
}

.dots-spacer {
  width: 70px;
}

.term-body { 
  padding: 1.5rem 2rem; 
  min-height: 400px;
  max-height: 60vh;
  overflow-y: auto;
  background: var(--tui-bg);
}

.term-prompt { 
  margin-bottom: 1rem; 
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  font-size: 0.95rem;
}

.term-user { 
  color: #33ff66; 
  font-weight: 700;
  text-shadow: 0 0 8px rgba(51,255,102,0.5);
}

.term-at { 
  color: #ffffff; 
  margin: 0 0.1em; 
  font-weight: 600;
}

.term-host { 
  color: #33ff66; 
  font-weight: 700;
  text-shadow: 0 0 8px rgba(51,255,102,0.5);
}

.term-sep { 
  color: #ffffff; 
  margin: 0 0.2em;
  font-weight: 600;
}

.term-path { 
  color: #66ccff; 
  font-weight: 700;
  text-shadow: 0 0 8px rgba(102,204,255,0.5);
}

.term-dollar { 
  color: #ffffff; 
  margin: 0 0.4em;
  font-weight: 700;
}

.term-content {
  font-size: 0.9rem;
  line-height: 1.7;
}

.terminal-statusbar {
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
  font-weight: 600;
  padding: 0 1.2rem;
  z-index: 9999;
  font-family: var(--tui-font);
  border-top: 1px solid rgba(255,255,255,0.1);
  box-shadow: 0 -2px 10px rgba(51,255,102,0.3);
}

.terminal-statusbar .left,
.terminal-statusbar .right {
  display: flex;
  gap: 0.8rem;
  align-items: center;
}

.terminal-statusbar .center {
  flex: 1;
}

.status-item {
  font-weight: 600;
  letter-spacing: 0.02em;
}

.status-item.shell {
  background: var(--tui-bg);
  color: var(--tui-accent);
  padding: 0.2em 0.7em;
  border-radius: 3px;
  font-weight: 700;
  text-shadow: 0 0 4px rgba(51,255,102,0.6);
  border: 1px solid rgba(51,255,102,0.3);
}

.status-item.page {
  font-weight: 700;
  letter-spacing: 0.05em;
}

.separator {
  opacity: 0.5;
  font-weight: 400;
  margin: 0 0.2rem;
}

/* Scrollbar styling */
.term-body::-webkit-scrollbar {
  width: 8px;
}

.term-body::-webkit-scrollbar-track {
  background: rgba(0,0,0,0.3);
  border-radius: 4px;
}

.term-body::-webkit-scrollbar-thumb {
  background: var(--tui-fg-dim);
  border-radius: 4px;
}

.term-body::-webkit-scrollbar-thumb:hover {
  background: var(--tui-fg);
}
</style>
