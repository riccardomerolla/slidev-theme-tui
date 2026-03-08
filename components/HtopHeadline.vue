<template>
  <h1 class="htop-headline">{{ resolvedTitle }}</h1>
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  title?: string
}>()

const resolvedTitle = computed(() => props.title?.trim() || 'Il Livello Successivo: Autonomia con Agent AI')
</script>

<style scoped>
.htop-headline {
  margin: 0;
  color: #50ff74;
  text-shadow: 0 0 10px rgba(80, 255, 116, 0.55);
  font-size: clamp(1.35rem, 3vw, 2.2rem);
  line-height: 1.05;
  font-weight: 800;
}
</style>
