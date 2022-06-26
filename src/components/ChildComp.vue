<script setup lang="ts">
const props = defineProps({
    msg: String
})

</script>

<template>
    <div class="row">
        <h2>{{ msg ?? 'No props passed yet' }}</h2>
    </div>
</template>

<style scoped>
</style>