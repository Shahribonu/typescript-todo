<template>
  <div id="app">
    <AppHeader />
    <AppFilters :setFilter="setFilter" :filter="filter" />

    <main class="app-main">
      <AppTodoList
        :todos="filteredTodos"
        @remove-todo="removeTodo"
        @toggle-todo="toggleTodo"
      />
      <AppAddTodo @add-todo="addTodoList" />
    </main>

    <AppFooter />
  </div>
</template>

<script lang="ts" setup>
import { ref, computed, onMounted } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFilters from "./components/AppFilters.vue";
import AppTodoList from "./components/AppTodoList.vue";
import AppFooter from "./components/AppFooter.vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import type { Todo } from "@/types/todo";
const filter = ref("all");
interface State {
  todos: Todo[];
}
const todos = ref<State["todos"]>([
  { id: 0, text: "Learn Typescript", completed: true },
  { id: 1, text: "Learn Nuxt", completed: true },
  { id: 2, text: "Learn Pinia", completed: false },
  { id: 3, text: "Learn smth", completed: false },
]);

const setFilter = (newFilter: string) => {
  filter.value = newFilter;
  localStorage.setItem("filter", filter.value);
};

onMounted(() => {
  const storedTodos = JSON.parse(localStorage.getItem("todos") || "[]");
  todos.value = storedTodos;

  const storedFilter = localStorage.getItem("filter");
  if (storedFilter) {
    filter.value = storedFilter;
  }
});

const filteredTodos = computed(() => {
  switch (filter.value) {
    case "completed":
      return todos.value.filter((todo) => todo.completed);
    case "active":
      return todos.value.filter((todo) => !todo.completed);
    default:
      return todos.value;
  }
});

const toggleTodo = (id: number) => {
  const targetTodo = todos.value.find((todo: Todo) => todo.id == id);
  if (targetTodo) {
    targetTodo.completed = !targetTodo.completed;
    localStorage.setItem("todos", JSON.stringify(todos.value));
  }
};
const removeTodo = (id: number) => {
  todos.value = todos.value.filter((todo: Todo) => todo.id !== id);
  localStorage.setItem("todos", JSON.stringify(todos.value));
};
const addTodoList = (data: Todo) => {
  todos.value = [...todos.value, data];
  localStorage.setItem("todos", JSON.stringify(todos.value));
  console.log(todos.value, "todos");
};
</script>
