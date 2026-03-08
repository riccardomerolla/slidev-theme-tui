<template>
  <div class="slidev-layout cover">
    <div class="bg-scanlines"></div>
    <div class="bg-vignette"></div>
    <div class="bg-matrix"></div>
    <div class="bg-phosphor"></div>
    <div class="cover-content">
      <div class="cover-ascii-art">
        <pre>┌────────────────────────────┐
│ slidev-theme-tui v0.1.0    │
│ Terminal Presentation      │
└────────────────────────────┘</pre>
      </div>
      <div class="cover-title">
        <slot name="default" />
      </div>
      <div class="cover-meta">
        <slot name="info" />
      </div>
      <div class="cover-prompt">
        <span class="prompt-dollar">$</span>
        <span class="prompt-command">slidev present</span>
        <span class="cursor-blink">█</span>
      </div>
    </div>
    <div class="cover-statusbar">
      <span class="left">
        <span class="mode-indicator">READY</span>
        <span class="separator">│</span>
        <span class="filename">presentation.md</span>
      </span>
      <span class="center"></span>
      <span class="right">
        <span class="timestamp">{{ new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' }) }}</span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.cover {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.cover-content {
  text-align: center;
  z-index: 10;
  position: relative;
  max-width: 90%;
  margin: 0 auto;
}

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes glow-pulse {
  0%, 100% { 
    text-shadow: 0 0 10px rgba(51,255,102,0.6),
                 0 0 20px rgba(51,255,102,0.4),
                 0 0 30px rgba(51,255,102,0.2);
  }
  50% { 
    text-shadow: 0 0 15px rgba(51,255,102,0.9),
                 0 0 30px rgba(51,255,102,0.6),
                 0 0 45px rgba(51,255,102,0.3);
  }
}

.cover-ascii-art {
  margin-bottom: 2rem;
  animation: fadeInUp 0.7s ease-out;
}

.cover-ascii-art pre {
  color: var(--tui-accent);
  font-size: 0.65rem;
  line-height: 1.3;
  text-shadow: 0 0 8px rgba(51,255,102,0.5);
  font-weight: 500;
  letter-spacing: 0.05em;
}

.cover-title {
  font-size: 3rem;
  font-weight: 700;
  color: var(--tui-accent);
  text-shadow: 0 0 20px rgba(51,255,102,0.8),
               0 0 40px rgba(51,255,102,0.4);
  margin: 1.5rem 0 1rem;
  line-height: 1.3;
  animation: fadeInUp 0.8s ease-out 0.2s both, glow-pulse 3s ease-in-out infinite;
  letter-spacing: -0.02em;
}

.cover-meta {
  color: var(--tui-fg);
  font-size: 1.1rem;
  line-height: 1.7;
  animation: fadeInUp 0.8s ease-out 0.4s both;
  max-width: 80%;
  margin: 0 auto;
  text-shadow: 0 0 8px rgba(51,255,102,0.3);
}

.cover-prompt {
  margin-top: 2.5rem;
  animation: fadeInUp 0.8s ease-out 0.6s both;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1.1rem;
  padding: 0.8rem 1.5rem;
  background: rgba(51,255,102,0.05);
  border: 1px solid rgba(51,255,102,0.2);
  border-radius: 4px;
}

.prompt-dollar {
  color: var(--tui-accent);
  font-weight: 700;
  text-shadow: 0 0 10px rgba(51,255,102,0.8);
  font-size: 1.2em;
}

.prompt-command {
  color: var(--tui-fg);
  text-shadow: 0 0 6px rgba(51,255,102,0.4);
  font-weight: 500;
}

.cursor-blink {
  color: var(--tui-accent);
  animation: blink 1.2s step-start infinite;
  text-shadow: 0 0 8px rgba(51,255,102,0.8);
  font-size: 0.9em;
  margin-left: 0.2em;
}

@keyframes blink {
  0%, 49% { opacity: 1; }
  50%, 100% { opacity: 0; }
}

.cover-statusbar {
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

.cover-statusbar .left,
.cover-statusbar .right {
  display: flex;
  gap: 0.8rem;
  align-items: center;
}

.cover-statusbar .center {
  flex: 1;
}

.mode-indicator {
  background: var(--tui-bg);
  color: var(--tui-accent);
  padding: 0.2em 0.7em;
  border-radius: 3px;
  font-weight: 700;
  letter-spacing: 0.05em;
  font-size: 0.85em;
  text-shadow: 0 0 4px rgba(51,255,102,0.6);
  border: 1px solid rgba(51,255,102,0.3);
}

.separator {
  opacity: 0.5;
  font-weight: 400;
}

.filename {
  font-weight: 500;
  letter-spacing: 0.02em;
}

.timestamp {
  font-weight: 500;
  opacity: 0.9;
  font-size: 0.9em;
}

.cover-prompt {
  animation: fadeInUp 0.8s ease-out 0.6s both;
}
</style>
