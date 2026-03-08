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
  gap: 1rem; 
  margin: 1rem 0;
}

.gemini-prompt-wrap {
  background: rgba(129,140,248,0.08);
  border: 1px solid rgba(129,140,248,0.25);
  border-radius: 6px;
  padding: 0.8rem 1rem;
  transition: all 0.2s ease;
}

.gemini-prompt-wrap:hover {
  background: rgba(129,140,248,0.12);
  border-color: rgba(129,140,248,0.35);
}

.gemini-prompt-prefix {
  color: #818cf8;
  font-weight: 700;
  margin-right: 0.6em;
  text-shadow: 0 0 10px rgba(129,140,248,0.9);
  font-size: 1.1em;
}

.gemini-prompt-text { 
  color: #e2e8f0; 
  font-size: 0.95rem; 
  line-height: 1.5;
}

.gemini-thinking {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  color: #818cf8;
  font-size: 0.85rem;
  font-style: italic;
  padding: 0.5rem 0;
}

.gemini-thinking-dots {
  display: inline-flex;
  gap: 3px;
}

.gemini-thinking-dots span {
  display: inline-block;
  width: 5px; 
  height: 5px;
  background: #818cf8;
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
  padding: 1rem 1.2rem;
  border-left: 3px solid #34d399;
  background: linear-gradient(
    to right, 
    rgba(52,211,153,0.06) 0%, 
    rgba(52,211,153,0.02) 100%
  );
  border-radius: 0 4px 4px 0;
}

.gemini-response-prefix {
  font-size: 0.72rem;
  color: #34d399;
  font-weight: 700;
  margin-bottom: 0.6rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  text-shadow: 0 0 8px rgba(52,211,153,0.5);
}

.gemini-response-content {
  color: #e2e8f0;
  line-height: 1.6;
}

.gemini-response-content p {
  margin: 0.5rem 0;
}

.gemini-response-content code {
  background: rgba(129,140,248,0.15);
  padding: 0.15em 0.4em;
  border-radius: 3px;
  font-size: 0.9em;
  color: #818cf8;
}

.gemini-tool {
  background: linear-gradient(
    135deg,
    rgba(96,165,250,0.08) 0%,
    rgba(96,165,250,0.04) 100%
  );
  border: 1px solid rgba(96,165,250,0.3);
  border-radius: 6px;
  padding: 0.7rem 0.9rem;
  margin-top: 0.5rem;
  font-size: 0.85rem;
}

.gemini-tool-name {
  color: #60a5fa;
  font-weight: 700;
  font-size: 0.72rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.4rem;
  text-shadow: 0 0 8px rgba(96,165,250,0.5);
}

.gemini-tool-content {
  color: rgba(226,232,240,0.8);
  font-size: 0.85rem;
}
  letter-spacing: 0.08em;
  margin-bottom: 0.2rem;
}
.gemini-tool-name::before { content: 'TOOL: '; }
</style>
