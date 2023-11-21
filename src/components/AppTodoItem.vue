<template>
  <li
    class="todo-item"
    :class="{ 'todo-item--done': todo.completed }"
    @click="toggleTodo(todo)"
  >
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo(todo)">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts" setup>
import { defineProps, type PropType } from "vue";
import type { Todo } from "../types/todo";
const emits = defineEmits();

const props = defineProps({
  todo: {
    type: Object as PropType<Todo>,
    required: true,
  },
});

const toggleTodo = (todo: Todo) => {
  console.log(todo);
  emits("toggleTodo", todo.id);
};

const removeTodo = (todo: Todo) => {
  emits("removeTodo", todo.id);
};
</script>
