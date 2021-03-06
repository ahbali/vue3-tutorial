<script setup lang="ts">
  import { computed, onMounted, reactive, Ref, ref, watch } from 'vue'
  import ChildComp from './components/ChildComp.vue'
  const counter = reactive({
    count: 0,
  })
  console.log(counter.count)
  counter.count++

  const message = ref('hello world')
  console.log(message.value)
  message.value = 'changed'

  const text = reactive({
    message: 'hellooooo',
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
  // part 8: computed Property
  type Todo = {
    id: number
    text: string
    done: boolean
  }
  let id = 0
  const newTodo = ref('')
  const hideCompleted = ref(false)
  const todos: Ref<Array<Todo>> = ref([
    { id: id++, text: 'Learn HTML', done: true },
    { id: id++, text: 'Learn JavaScript', done: true },
    { id: id++, text: 'Learn Vue', done: false },
  ])

  function addTodo() {
    todos.value = [
      ...todos.value,
      { id: id++, text: newTodo.value, done: false },
    ]
    newTodo.value = ''
  }
  function removeTodo(todo: Todo) {
    todos.value = todos.value.filter((old) => old.id !== todo.id)
  }
  const filteredTodos = computed(() => {
    return hideCompleted.value
      ? todos.value.filter((todo) => todo.done === false)
      : todos.value
  })
  // part 9: Lifecycle and Template Refs
  const p = ref<HTMLParagraphElement>()
  onMounted(() => {
    if (p.value?.textContent) {
      p.value.textContent = 'onMounted value'
    }
  })
  // part 10: Watchers
  const count10 = ref(0)
  watch(count10, (newCount) => {
    console.log(`new count is : ${newCount}`)
  })
  const todoId = ref(1)
  const todoData = ref(null)

  async function fetchData() {
    todoData.value = null
    const res = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
    )
    todoData.value = await res.json()
  }

  fetchData()
  watch(todoId, fetchData)
  // part 12: Props
  const greeting = ref('Message from parent via Props')
  // part 13: Emits
  const childMsg = ref('No child msg yet')
  // part 14: Slots
  const parentMsg = ref('Message from the parent via Slots')
</script>

<template>
  <div class="col">
    <div class="row">
      <div class="col-6">
        <h1>assignment: {{ text.message }}</h1>
        <h1>{{ message.split('').reverse().join('') }}</h1>
        <p>count is: {{ counter.count }}</p>
        <h1 :class="titleClass">make me red</h1>
        <button class="btn btn-primary" @click="increment">
          count is: {{ count }}
        </button>
        <input :value="newText" placeholder="try to type" @input="onInput" />
        <input v-model="newText" placeholder="Type here" />
        <p>{{ newText }}</p>
      </div>
    </div>
    <!-- part 6: conditional rendering -->
    <div class="row">
      <div class="col-6">
        <h1>part 6: conditional rendering</h1>
        <button class="btn btn-danger" @click="toggle">toggle</button>
        <h3 v-if="awesome">Vue is awesome!</h3>
        <h3 v-else>Oh no :`(</h3>
      </div>
    </div>

    <!-- part 7: List Rendering -->
    <!-- part 8: computed Property -->
    <div class="row">
      <div class="col-6">
        <h1>part 7: List Rendering</h1>
        <h1>part 8: computed Property</h1>
        <form @submit.prevent="addTodo">
          <input v-model="newTodo" placeholder="put your todo here" />
          <button>Add Todo</button>
        </form>
        <ul>
          <li v-for="todo in filteredTodos" :key="todo.id">
            <input v-model="todo.done" type="checkbox" />
            <span :class="{ done: todo.done }">
              {{ todo.text }}
            </span>
            <button @click="removeTodo(todo)">X</button>
          </li>
        </ul>
        <button @click="hideCompleted = !hideCompleted">
          {{ hideCompleted ? 'Show all' : 'Hide completed' }}
        </button>
      </div>
    </div>
    <!-- part 9: Lifecycle and Template Refs -->
    <div class="row">
      <p ref="p">initial value</p>
    </div>
    <!-- part 10: Watchers -->
    <div class="row">
      <div class="col-6">
        <button @click="count10++">increment</button>
      </div>
    </div>
    <div class="row">
      <div class="col-10">
        <p>Todo id: {{ todoId }}</p>
        <button @click="todoId++">Fetch next todo</button>
        <p v-if="!todoData">Loading...</p>
        <pre v-else>{{ todoData }}</pre>
      </div>
    </div>
  </div>
  <!-- part 11: Components -->
  <!-- part 12: Props -->
  <!-- part 13: Emits -->
  <ChildComp :msg="greeting" @response="(msg) => (childMsg = msg)">
    <!-- part 14: Slots -->
    <h3>{{ parentMsg }}</h3>
  </ChildComp>
  <p>{{ childMsg }}</p>
</template>

<style>
  .title {
    color: red;
  }

  .done {
    text-decoration: line-through;
  }
</style>
