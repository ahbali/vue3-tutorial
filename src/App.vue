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

const titleClass = ref('title')
const count = ref(0)

function increment() {
    count.value++
}

const newText = ref('')
function onInput(e: Event) {
    const elm = e.target as HTMLInputElement
    newText.value = elm.value
}
</script>

<template>
    <div class="col">
        <h1>assignment: {{ text.message }}</h1>
        <h1>{{ message.split('').reverse().join('') }}</h1>
        <p>count is: {{ counter.count }}</p>
        <h1 :class="titleClass">make me red</h1>
        <button @click="increment" class="btn btn-primary">count is: {{ count }}</button>
        <input :value="newText" @input="onInput" placeholder="try to type">
        <input v-model="newText" placeholder="Type here">
        <p>{{ newText }}</p>
    </div>
</template>

<style>
.title {
    color: red;
}
</style>
