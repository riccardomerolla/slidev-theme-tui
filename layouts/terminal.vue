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
.terminal { display: flex; align-items: center; justify-content: center; }
.term-window {
  width: 90%; max-height: 85%;
  border: 1px solid var(--tui-border);
  box-shadow: 0 0 30px rgba(51,255,102,0.15), inset 0 0 30px rgba(0,0,0,0.5);
  overflow: hidden;
}
.term-titlebar {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.4rem 0.8rem;
  background: #1c1c1c;
  border-bottom: 1px solid var(--tui-border);
}
.dot { width: 10px; height: 10px; border-radius: 50%; }
.dot.red    { background: #ff5f57; }
.dot.yellow { background: #febc2e; }
.dot.green  { background: #28c840; }
.term-title { margin-left: 0.5rem; font-size: 0.75rem; color: #666; flex: 1; text-align: center; }
.term-body { padding: 1rem; min-height: 60%; }
.term-prompt { margin-bottom: 0.5rem; }
.term-user   { color: #33ff66; font-weight: 700; }
.term-sep    { color: #ffffff; }
.term-path   { color: #66ccff; font-weight: 700; }
.term-dollar { color: #ffffff; margin-left: 0.1em; margin-right: 0.5em; }
</style>
