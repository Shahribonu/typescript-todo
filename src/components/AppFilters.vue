<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        class="button"
        :class="{ 'button--primary': props.filter === 'all' }"
        @click="handleFilter('all')"
      >
        All
      </button>
      <button
        class="button"
        :class="{ 'button--primary': props.filter === 'active' }"
        @click="handleFilter('active')"
      >
        Active
      </button>
      <button
        class="button"
        :class="{ 'button--primary': props.filter === 'completed' }"
        @click="handleFilter('completed')"
      >
        Completed
      </button>
    </section>
  </aside>
</template>

<script lang="ts" setup>
import { defineProps } from "vue";
const props = defineProps(["setFilter", "filter"]);

const handleFilter = (filterValue: string) => {
  props.setFilter(filterValue);
};
</script>
