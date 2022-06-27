<script setup lang="ts">
  // part 12: Props
  const props = defineProps<{
    msg?: string
  }>()
  // part 13: Emits
  const emit = defineEmits<{
    (event: 'response', msg: string): void
  }>()
  emit('response', 'hello from child')
</script>

<template>
  <div class="row">
    <h2>{{ msg ?? 'No props passed yet' }}</h2>
  </div>
  <!-- part 14: Slots -->
  <slot>Fallback content</slot>
</template>

<style scoped></style>
