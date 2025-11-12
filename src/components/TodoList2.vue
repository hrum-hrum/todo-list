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
        :todo="todo"
        @remove-todo="() => $emit('remove-todo', index)"
        @complete-todo.once="() => $emit('complete-todo', todo)"
      />

  </ul>
  <div v-if="!todos.length" class="todo-list__empty">
    <p>Список задач пуст</p>
  </div>
</template>
