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

const message = ref("hello world")
console.log(message.value)
message.value = 'changed'

const text = reactive({
    message: 'hellooooo'
})
</script>

<template>
    <h1>assignment: {{ text.message }}</h1>
    <h1>{{ message.split('').reverse().join('') }}</h1>
    <p>count is: {{ counter.count }}</p>
</template>

<style>
</style>
