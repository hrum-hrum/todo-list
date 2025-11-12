<script setup>
defineProps({
  remainingTodos: Number,
})
</script>

<template>
  <div class="todo-app__footer">
    <p class="todo-app__footer-text">Осталось {{ remainingTodos }} задания(й)</p>
    <button class="btn btn--clear" :disabled="false" @click="$emit('clear-completed')">
      Удалить завершенные
    </button>
    <button class="btn btn--clear" :disabled="false" @click="$emit('clear-all')">
      Очистить список
    </button>
  </div>
</template>
