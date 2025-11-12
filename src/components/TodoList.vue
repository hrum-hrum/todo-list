<script setup>
import TodoListItem from './TodoListItem.vue'

defineProps({
  todos: {
    type: Array,
    requred: true,
  },
})
</script>

<template>
  <ul class="todo-list">
    <TodoListItem
      v-for="(todo, index) in todos"
      :key="`todo_${todo.id}`"
      v-bind="todo"
      @complete-todo="() => $emit('complete-todo', todo)"
      @remove-todo="() => $emit('remove-todo', index)"
    />
  </ul>
  <div v-if="!todos.length" class="todo-list__empty">
    <p>Список задач пуст</p>
  </div>
</template>
