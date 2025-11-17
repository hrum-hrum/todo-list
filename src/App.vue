<script setup>
import { reactive, computed } from 'vue'

import TodoFooter from './components/TodoFooter.vue'
import TodoList from './components/TodoList.vue'
import TodoForm from './components/TodoForm.vue'

let todos = reactive([
  {
    id: 1,
    text: 'Изучить компоненты Vue.js',
    completed: false,
  },
  {
    id: 2,
    text: 'Создать TodoList приложение',
    completed: false,
  },
  {
    id: 3,
    text: 'Похвалить себя за отличную работу',
    completed: false,
  },
])

function completeTodo(todo) {
  todo.completed = true
  // alert('Завершено')
}

const removeTodo = (index) => {
  //Не работает
  //todos = todos.filter((item) => item.id != todo.id)
  todos.splice(index, 1)
}

const addTodo = (todoTitle) => {
  todos.push({
    id: Date.now(),
    text: todoTitle,
    completed: false,
  })
}

function clearCompleted() {
  //Не работает
  // todos.forEach((todo, index) => {
  //   if (todo.completed) todos.splice(index, 1)
  // })

  for (let i = todos.length - 1; i >= 0; i--) {
    if (todos[i].completed) todos.splice(i, 1)
  }
}

function clearAll() {
  todos.splice(0, todos.length)
}

const remainingTodos = computed(() => {
  return todos.filter((todo) => !todo.completed).length
})
</script>

<template>
  <main>
    <div class="container todo-app">
      <h1 class="title">Todo List</h1>
      <TodoForm @add-todo="addTodo" />
      <TodoList :todos="todos" @complete-todo="completeTodo" @remove-todo="removeTodo" />
      <TodoFooter
        v-if="todos.length"
        :remaining-todos="remainingTodos"
        @clear-all="clearAll"
        @clear-completed="clearCompleted"
      />
    </div>
  </main>
</template>

<style src="./App.css"></style>
