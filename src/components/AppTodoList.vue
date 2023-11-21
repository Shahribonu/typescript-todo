<template>
  <ul class="todo-list">
    <AppTodoItem
      v-for="todo in todos"
      id="todo.id"
      :todo="todo"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
  </ul>
</template>

<script lang="ts" setup>
import { ref, type PropType, defineProps, defineEmits } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import type { Todo } from "@/types/todo";
const emits = defineEmits();

const props = defineProps({
  todos: {
    type: Object as PropType<Todo[]>,
    required: true,
  },
});

const toggleTodo = (id: number) => {
  emits("toggleTodo", id);
};

const removeTodo = (id: number) => {
  emits("removeTodo", id);
};
</script>

<style scoped></style>
