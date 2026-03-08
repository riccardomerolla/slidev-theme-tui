<template>
  <div class="slidev-layout nano">
    <div class="bg-scanlines"></div>
    <div class="bg-ascii"></div>
    <!-- Nano top bar -->
    <div class="nano-topbar">
      <span class="nano-version">GNU nano 5.3</span>
      <span class="nano-filename">{{ filename }}</span>
    </div>
    <!-- Content area with border -->
    <div class="nano-border-top"></div>
    <div class="nano-content">
      <slot />
    </div>
    <div class="nano-border-bottom"></div>
    <!-- Nano help bar -->
    <div class="nano-helpbar">
      <div class="nano-help-row">
        <span class="nano-help-item"><span class="nano-help-key">^G</span><span class="nano-help-label">Help</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^O</span><span class="nano-help-label">Write Out</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^R</span><span class="nano-help-label">Where Is</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^K</span><span class="nano-help-label">Cut Text</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^J</span><span class="nano-help-label">Justify</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^C</span><span class="nano-help-label">Go To Line</span></span>
      </div>
      <div class="nano-help-row">
        <span class="nano-help-item"><span class="nano-help-key">^X</span><span class="nano-help-label">Exit</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^R</span><span class="nano-help-label">Read File</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^\</span><span class="nano-help-label">Replace</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^U</span><span class="nano-help-label">Uncut Text</span></span>
        <span class="nano-help-item"><span class="nano-help-key">^T</span><span class="nano-help-label">To Spell</span></span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useSlideContext } from '@slidev/client'

const { $slidev } = useSlideContext()

const filename = computed(() => {
  return `presentation.md (Line ${$slidev.nav.currentPage}, Col 1)`
})
</script>

<style scoped>
.nano {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 100%;
  background: #000000;
  color: #00ffff;
  font-family: 'JetBrains Mono', 'Fira Code', monospace;
  display: flex;
  flex-direction: column;
  font-size: 0.9rem;
  line-height: 1.5;
}

.nano-topbar {
  flex-shrink: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #00ffff;
  color: #000000;
  padding: 0.5rem 1.2rem;
  font-weight: 700;
  border-bottom: 2px solid #00ffff;
  box-shadow: 0 2px 12px rgba(0, 255, 255, 0.3);
  letter-spacing: 0.05em;
}

.nano-version {
  font-size: 0.9rem;
  text-transform: uppercase;
}

.nano-filename {
  font-size: 0.9rem;
  text-align: right;
}

.nano-border-top {
  flex-shrink: 0;
  height: 1.2rem;
  background: #000000;
  border-bottom: 2px dashed #00ffff;
  position: relative;
}

.nano-border-top::before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 100%;
  color: #00ffff;
  text-align: left;
  letter-spacing: 0.05em;
  font-size: 0.8rem;
}

.nano-border-bottom {
  flex-shrink: 0;
  height: 1.2rem;
  background: #000000;
  border-top: 2px dashed #00ffff;
}

.nano-border-bottom::before {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  color: #00ffff;
  text-align: left;
  letter-spacing: 0.05em;
}

.nano-content {
  flex: 1;
  min-height: 0;
  padding: 2rem 2.5rem;
  overflow-y: auto;
  background: #000000;
  color: #00ffff;
  border-left: 2px dashed #00ffff;
  border-right: 2px dashed #00ffff;
}

.nano-content :deep(h1),
.nano-content :deep(h2),
.nano-content :deep(h3) {
  color: #00ffff;
  text-shadow: 0 0 15px rgba(0, 255, 255, 0.5), 0 0 30px rgba(0, 255, 255, 0.25);
  margin: 1.5rem 0 1rem 0;
  font-weight: 700;
  letter-spacing: 0.05em;
}

.nano-content :deep(h1) {
  font-size: 2rem;
}

.nano-content :deep(h2) {
  font-size: 1.6rem;
}

.nano-content :deep(h3) {
  font-size: 1.3rem;
}

.nano-content :deep(p) {
  margin: 0.8rem 0;
  color: #00ffff;
  font-size: 0.95rem;
  font-weight: 500;
}

.nano-content :deep(strong) {
  color: #ffff00;
  text-shadow: 0 0 8px rgba(255, 255, 0, 0.4);
}

.nano-content :deep(em) {
  color: #00ff99;
  font-style: italic;
}

.nano-content :deep(code) {
  background: rgba(0, 0, 0, 0.5);
  color: #ffff00;
  padding: 0.2em 0.5em;
  border-radius: 0px;
  font-family: inherit;
  border: 1px solid #00ffff;
  text-shadow: 0 0 4px rgba(255, 255, 0, 0.3);
  font-weight: 600;
}

.nano-content :deep(pre) {
  background: rgba(0, 0, 0, 0.6);
  color: #00ff99;
  padding: 1.2rem;
  border: 2px solid #00ffff;
  border-left: 4px solid #ffff00;
  border-radius: 0px;
  overflow-x: auto;
  margin: 1.5rem 0;
  box-shadow: inset 0 0 20px rgba(0, 255, 255, 0.1), 0 0 15px rgba(0, 255, 255, 0.15);
}

.nano-content :deep(pre code) {
  background: none;
  border: none;
  padding: 0;
  color: #00ff99;
  text-shadow: 0 0 6px rgba(0, 255, 102, 0.3);
}

.nano-content :deep(blockquote) {
  border-left: 4px solid #ffff00;
  padding-left: 1.5rem;
  margin: 1.5rem 0;
  color: #00ffff;
  font-style: italic;
  background: rgba(255, 255, 0, 0.05);
  padding: 1rem 1rem 1rem 1.5rem;
}

.nano-content :deep(ul),
.nano-content :deep(ol) {
  margin: 1rem 0;
  padding-left: 2.5rem;
}

.nano-content :deep(li) {
  margin: 0.6rem 0;
  color: #00ffff;
  font-weight: 500;
}

.nano-helpbar {
  flex-shrink: 0;
  background: #00ffff;
  color: #000000;
  padding: 0.38rem 1.2rem 0.32rem;
  font-size: 0.8rem;
  font-weight: 700;
  border-top: 2px solid #00ffff;
  box-shadow: 0 -3px 12px rgba(0, 255, 255, 0.3);
  line-height: 1.25;
  letter-spacing: 0.01em;
  display: flex;
  flex-direction: column;
  gap: 0.28rem;
}

.nano-help-row {
  display: grid;
  grid-template-columns: repeat(6, minmax(0, 1fr));
  column-gap: 1.1rem;
  row-gap: 0.35rem;
  padding: 0;
  align-items: center;
}

.nano-help-item {
  display: inline-flex;
  align-items: center;
  gap: 0.34rem;
  text-transform: none;
  letter-spacing: 0;
  white-space: nowrap;
  font-weight: 700;
  color: #000000;
  min-width: 0;
}

.nano-help-key {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 2ch;
  height: 1.18em;
  padding: 0 0.2em;
  background: #002a2f;
  color: #00ffff;
  border: 1px solid rgba(0, 0, 0, 0.55);
  box-shadow: inset 0 0 0 1px rgba(0, 255, 255, 0.35);
  font-size: 0.95em;
  line-height: 1;
}

.nano-help-label {
  color: #000000;
  text-transform: uppercase;
  letter-spacing: 0.035em;
}

@media (max-width: 900px) {
  .nano-help-row {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
}
</style>
