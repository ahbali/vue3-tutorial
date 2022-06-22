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
// part 6: conditional Rendering
const awesome = ref(true)
function toggle() {
    awesome.value = !awesome.value
}
// part 7: List Rendering
type Todo = {
    id: number;
    text: string;
}
let id = 0
const newTodo = ref('')
const todos = ref([
    { id: id++, text: 'Learn HTML' },
    { id: id++, text: 'Learn JavaScript' },
    { id: id++, text: 'Learn Vue' }
])

function addTodo(e: Event) {
    todos.value = [{ id: id++, text: newTodo.value }, ...todos.value]
    newTodo.value = ''
}
function removeTodo(todo: Todo) {
    todos.value = todos.value.filter(old => old.id !== todo.id)
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
        <!-- part 6: conditional rendering -->
        <button class="btn btn-danger" @click="toggle">toggle</button>
        <h1 v-if="awesome">Vue is awesome!</h1>
        <h1 v-else>Oh no :`(</h1>

        <!-- part 7: List Rendering -->
        <form @submit.prevent="addTodo">
            <input v-model="newTodo">
            <button>Add Todo</button>
        </form>
        <ul>
            <li v-for="todo in todos" :key="todo.id">
                {{ todo.text }}
                <button @click="removeTodo(todo)">X</button>
            </li>
        </ul>
    </div>
</template>

<style>
.title {
    color: red;
}
</style>
