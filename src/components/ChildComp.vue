<script setup lang="ts">
// part 12: Props
const props = defineProps<{
    msg?: String
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
</template>

<style scoped>
</style>