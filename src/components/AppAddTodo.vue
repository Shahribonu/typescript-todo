<template>
  <section class="add-todo">
    <button
      class="add-todo__show-form-button"
      v-if="!isFormVisible"
      @click="toggleForm"
    >
      <i class="bi bi-plus-lg"></i>
    </button>
    <form class="add-todo__form" v-if="isFormVisible" @submit.prevent="AddTodo">
      <button class="close-button" type="button" @click="toggleForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="todoText" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
  </section>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { defineEmits } from "vue";

const emits = defineEmits();
interface State {
  isFormVisible: boolean;
  todoText: string;
}
const isFormVisible = ref<State["isFormVisible"]>(false);
const todoText = ref<State["todoText"]>("");

const toggleForm = () => {
  isFormVisible.value = !isFormVisible.value;
};

const AddTodo = () => {
  emits("add-todo", { id: Date.now(), text: todoText.value, completed: false });
  todoText.value = "";
};
</script>
