<template>
  <div class="gemini-exchange">
    <!-- User prompt -->
    <div class="gemini-prompt-wrap" v-if="prompt">
      <span class="gemini-prompt-prefix">&gt;</span>
      <span class="gemini-prompt-text">{{ prompt }}</span>
    </div>
    <!-- Thinking indicator -->
    <div v-if="thinking" class="gemini-thinking">
      <span>Thinking</span>
      <span class="gemini-thinking-dots">
        <span></span><span></span><span></span>
      </span>
    </div>
    <!-- AI Response -->
    <div class="gemini-response" v-if="!thinking">
      <div class="gemini-response-prefix">Gemini</div>
      <div class="gemini-response-content">
        <slot />
      </div>
    </div>
    <!-- Tool use -->
    <div v-if="tool" class="gemini-tool">
      <div class="gemini-tool-name">{{ tool }}</div>
      <div class="gemini-tool-content">
        <slot name="tool" />
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  prompt:  { type: String, default: '' },
  thinking: { type: Boolean, default: false },
  tool:    { type: String, default: '' },
  model:   { type: String, default: 'gemini-2.5-pro' },
})
</script>

<style scoped>
.gemini-exchange { 
  display: flex; 
  flex-direction: column; 
  gap: 0.8rem; 
  margin: 1.1rem 0 0.6rem;
  border-top: 1px solid rgba(129, 140, 248, 0.18);
  padding-top: 0.9rem;
}

.gemini-prompt-wrap {
  background: rgba(24, 31, 48, 0.72);
  border: 1px solid rgba(129, 140, 248, 0.24);
  border-radius: 0;
  padding: 0.6rem 0.75rem;
}

.gemini-prompt-prefix {
  color: #a5b4fc;
  font-weight: 700;
  margin-right: 0.5em;
  font-size: 1em;
  text-shadow: none;
}

.gemini-prompt-text { 
  color: #cfd6ea; 
  font-size: 0.9rem; 
  line-height: 1.45;
}

.gemini-thinking {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  color: #a5b4fc;
  font-size: 0.78rem;
  padding: 0.2rem 0;
}

.gemini-thinking-dots {
  display: inline-flex;
  gap: 3px;
}

.gemini-thinking-dots span {
  display: inline-block;
  width: 5px; 
  height: 5px;
  background: #a5b4fc;
  border-radius: 50%;
  animation: gemini-pulse 1.4s ease-in-out infinite;
}

.gemini-thinking-dots span:nth-child(2) { animation-delay: 0.2s; }
.gemini-thinking-dots span:nth-child(3) { animation-delay: 0.4s; }

@keyframes gemini-pulse {
  0%,80%,100% { transform: scale(0.6); opacity: 0.4; }
  40%          { transform: scale(1);   opacity: 1; }
}

.gemini-response {
  padding: 0.75rem 0.85rem;
  border-left: 2px solid rgba(16, 185, 129, 0.75);
  background: rgba(5, 18, 14, 0.42);
  border-radius: 0;
}

.gemini-response-prefix {
  font-size: 0.68rem;
  color: #34d399;
  font-weight: 700;
  margin-bottom: 0.45rem;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  text-shadow: none;
}

.gemini-response-content {
  color: #c9d2e5;
  line-height: 1.5;
}

.gemini-response-content p {
  margin: 0.35rem 0;
}

.gemini-response-content code {
  background: rgba(129,140,248,0.18);
  padding: 0.15em 0.4em;
  border-radius: 0;
  font-size: 0.9em;
  color: #c7d2fe;
}

.gemini-tool {
  background: rgba(12, 24, 40, 0.6);
  border: 1px solid rgba(96, 165, 250, 0.22);
  border-radius: 0;
  padding: 0.55rem 0.75rem;
  margin-top: 0.35rem;
  font-size: 0.8rem;
}

.gemini-tool-name {
  color: #60a5fa;
  font-weight: 700;
  font-size: 0.67rem;
  text-transform: uppercase;
  letter-spacing: 0.04em;
  margin-bottom: 0.25rem;
  text-shadow: none;
}

.gemini-tool-content {
  color: rgba(226,232,240,0.78);
  font-size: 0.8rem;
}

.gemini-tool-name::before { content: 'TOOL: '; }
</style>
