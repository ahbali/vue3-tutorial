<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
// import HelloWorld from './components/HelloWorld.vue'
import { reactive, ref } from 'vue';
const counter = reactive({
    count: 0
})
console.log(counter.count)
counter.count++

</script>

<template>
    <h1>Hello world</h1>
</template>

<style>
</style>
