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
      <slot />
    </div>
    <!-- Tool use -->
    <div v-if="tool" class="gemini-tool">
      <div class="gemini-tool-name">{{ tool }}</div>
      <slot name="tool" />
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
.gemini-exchange { display: flex; flex-direction: column; gap: 0.5rem; }
.gemini-prompt-wrap {
  background: rgba(129,140,248,0.05);
  border: 1px solid rgba(129,140,248,0.2);
  border-radius: 4px;
  padding: 0.6rem 0.8rem;
}
.gemini-prompt-prefix {
  color: #818cf8;
  font-weight: 700;
  margin-right: 0.5em;
  text-shadow: 0 0 8px rgba(129,140,248,0.8);
}
.gemini-prompt-text { color: #e2e8f0; font-size: 0.9rem; }
.gemini-thinking {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  color: #818cf8;
  font-size: 0.8rem;
  font-style: italic;
  padding: 0.3rem 0;
}
.gemini-thinking-dots span {
  display: inline-block;
  width: 4px; height: 4px;
  background: #818cf8;
  border-radius: 50%;
  margin: 0 1px;
  animation: gemini-pulse 1.4s ease-in-out infinite;
}
.gemini-thinking-dots span:nth-child(2) { animation-delay: 0.2s; }
.gemini-thinking-dots span:nth-child(3) { animation-delay: 0.4s; }
@keyframes gemini-pulse {
  0%,80%,100% { transform: scale(0.6); opacity: 0.4; }
  40%          { transform: scale(1);   opacity: 1; }
}
.gemini-response {
  padding: 0.8rem 1rem;
  border-left: 3px solid #34d399;
  background: rgba(52,211,153,0.04);
}
.gemini-response-prefix {
  font-size: 0.72rem;
  color: #34d399;
  font-weight: 700;
  margin-bottom: 0.4rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
.gemini-tool {
  background: #0d1b2a;
  border: 1px solid rgba(96,165,250,0.3);
  border-radius: 4px;
  padding: 0.5rem 0.7rem;
  margin-top: 0.3rem;
  font-size: 0.8rem;
}
.gemini-tool-name {
  color: #60a5fa;
  font-weight: 600;
  font-size: 0.72rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 0.2rem;
}
.gemini-tool-name::before { content: 'TOOL: '; }
</style>
