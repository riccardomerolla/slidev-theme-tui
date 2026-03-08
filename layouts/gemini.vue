<template>
  <div class="slidev-layout gemini layout-gemini">
    <div class="gemini-bg-gradient"></div>
    <div class="bg-scanlines" style="opacity: 0.2;"></div>

    <div class="gemini-body">
      <div class="gemini-hero">&gt;GEMINI</div>
      
      <div class="gemini-content">
        <slot />
      </div>
    </div>

    <div class="gemini-hintbar">shift+tab to accept edits</div>

    <div class="gemini-inputbar">
      <span class="prompt">&gt;</span>
      <span class="placeholder">Type your message or @path/to/file</span>
      <span class="context">1 GEMINI.md file</span>
    </div>

    <div class="gemini-statusbar">
      <span class="indicator">
        <span class="gemini-dot"></span>
        <span>Ready</span>
      </span>
      <span>{{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}</span>
      <span>/model Auto (Gemini 3)</span>
    </div>
  </div>
</template>

<style scoped>
.gemini {
  display: flex;
  flex-direction: column;
  min-height: 100%;
  height: 100%;
  width: 100%;
  background: #05070b;
  color: #c7ccda;
  position: relative;
  overflow: hidden;
  font-family: 'JetBrains Mono', 'Fira Code', monospace;
}

.gemini-body {
  flex: 1;
  min-height: 0;
  padding: 0.6rem 0.35rem 0.5rem 0.35rem;
  overflow-y: auto;
  position: relative;
  z-index: 1;
}

.gemini-cwd {
  color: #d1d5db;
  font-size: 0.75rem;
  margin-bottom: 0.4rem;
}

.gemini-hero {
  font-size: clamp(3.2rem, 10vw, 8rem);
  line-height: 0.9;
  font-weight: 900;
  letter-spacing: 0.02em;
  margin-bottom: 0.7rem;
  background: linear-gradient(90deg, #60a5fa 0%, #818cf8 50%, #f472b6 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  text-shadow: 0 0 18px rgba(129, 140, 248, 0.22);
}

.gemini-session-row {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
  font-size: 0.76rem;
  margin-bottom: 0.15rem;
  color: #e5e7eb;
}

.gemini-session-row .muted {
  color: #9ca3af;
}

.gemini-session-row .link {
  color: #818cf8;
}

.gemini-session-row .help {
  color: #7c84a0;
}

.gemini-content {
  margin-top: 0.95rem;
  padding-bottom: 0.6rem;
}

.gemini-content :deep(> *) {
  display: block;
}

.gemini-body :deep(h1),
.gemini-body :deep(h2),
.gemini-body :deep(h3) {
  color: #dce4ff;
  font-size: 1.1rem;
  margin: 0 0 0.55rem;
  text-shadow: none;
}

.gemini-body :deep(p),
.gemini-body :deep(li) {
  color: #cfd6ea;
  font-size: 0.92rem;
  line-height: 1.45;
}

.gemini-body :deep(ul),
.gemini-body :deep(ol) {
  margin-top: 0.5rem;
}

.gemini-hintbar {
  border-top: 1px solid rgba(129, 140, 248, 0.15);
  color: #8d97b7;
  font-size: 0.68rem;
  display: flex;
  align-items: center;
  padding: 0 0.8rem;
}

.gemini-inputbar {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  padding: 0 0.8rem;
  background: rgba(24, 31, 48, 0.8);
  border-top: 1px solid rgba(129, 140, 248, 0.18);
  border-bottom: 1px solid rgba(129, 140, 248, 0.18);
  font-size: 0.72rem;
}

.gemini-inputbar .prompt {
  color: #a5b4fc;
  font-weight: 700;
}

.gemini-inputbar .placeholder {
  color: #7f89a7;
  flex: 1;
}

.gemini-inputbar .context {
  color: #8d97b7;
}

.gemini-statusbar {
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding: 0 1rem;
  color: #d7dcee;
  background: linear-gradient(90deg, rgba(30, 41, 70, 0.9), rgba(21, 43, 67, 0.9));
  border-top: 1px solid rgba(129, 140, 248, 0.3);
  font-size: 0.75rem;
  position: relative;
  z-index: 2;
}

.gemini-statusbar .indicator {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
}

.gemini-dot {
  width: 8px;
  height: 8px;
  border-radius: 999px;
  background: #10b981;
  box-shadow: 0 0 5px rgba(16, 185, 129, 0.8);
  animation: gemini-dot-pulse 1.8s ease-in-out infinite;
}

.gemini-bg-gradient {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse at 12% 0%, rgba(99, 102, 241, 0.1) 0%, transparent 45%),
    radial-gradient(ellipse at 100% 100%, rgba(16, 185, 129, 0.07) 0%, transparent 45%);
  z-index: 0;
  pointer-events: none;
}

@keyframes gemini-dot-pulse {
  0%, 100% { opacity: 0.5; }
  50% { opacity: 1; }
}

@media (max-width: 900px) {
  .gemini-body {
    padding: 0.6rem 0.5rem 0.4rem;
  }

  .gemini-hero {
    font-size: clamp(2.6rem, 14vw, 4.8rem);
  }

  .gemini-statusbar span:nth-child(2),
  .gemini-inputbar .context,
  .gemini-session-row .help {
    display: none;
  }
}
</style>
