<script setup>
import { ref } from "vue";
import useTodos from "../composables/useTodos";

const { addTodo } = useTodos();

// Empty reference
const newTodo = ref("");
const add = () => {
  if (newTodo.value) {
    addTodo(newTodo.value);
    newTodo.value = "";
  }
};
</script>

<template>
  <h1 class="text-6xl font-medium tracking-tight text-center text-gray-100">
    Bryan's Todo App
  </h1>
  <input
    @change="add"
    v-model="newTodo"
    type="text"
    class="px-4 py-4 text-3xl text-center rounded-full"
    placeholder="Add a new item..."
  />
</template>
