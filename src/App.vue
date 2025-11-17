<script setup>
import { ref, reactive, computed } from 'vue'

import TodoFooter from './components/TodoFooter.vue'
import TodoList from './components/TodoList.vue'
import TodoForm from './components/TodoForm.vue'

const todoTitle = ref('test')
const todoTitle2 = ref('test2')

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

const todoInputChangeHandler = (title) => {
  todoTitle.value = title
}

const addTodo = () => {
  if (todoTitle.value) {
    const newTodoItem = {
      id: Date.now(),
      text: todoTitle.value,
      completed: false,
    }
    todos.push(newTodoItem)
    todoTitle.value = ''
  }
  if (todoTitle2.value) {
    const newTodoItem = {
      id: Date.now(),
      text: todoTitle2.value,
      completed: false,
    }
    todos.push(newTodoItem)
    todoTitle2.value = ''
  }
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
      <TodoForm
        :todo-title="todoTitle"
        @update:todo-title-input="todoInputChangeHandler"
        @submit:todo-form="addTodo"
        v-model="todoTitle2"
      />
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
