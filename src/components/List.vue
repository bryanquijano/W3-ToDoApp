<script setup>
import useTodos from "../composables/useTodos";

const { pending, changeStatus, completed } = useTodos();

defineProps({
  isCompleted: {
    default: false,
    type: Boolean,
  },
});
</script>

<template>
  <div class="w-1/3">
    <h3
      class="py-4 text-2xl text-center text-white rounded-md"
      :class="isCompleted ? 'bg-green-400' : 'bg-gray-400'"
    >
      {{ isCompleted ? "Completed" : "Pending" }}
    </h3>
    <ul class="pt-8 space-y-4">
      <li
        v-for="todo in isCompleted ? completed : pending"
        :key="todo.id"
        @click="changeStatus(todo.id)"
        class="w-full px-4 py-4 font-bold text-center duration-200 rounded-lg hover:cursor-pointer"
        :class="
          isCompleted
            ? 'text-green-600 bg-green-300 hover:bg-green-400 hover:text-green-200'
            : 'text-gray-600 bg-gray-300 hover:bg-gray-400 hover:text-gray-200'
        "
      >
        {{ todo.content }}
      </li>
    </ul>
  </div>
</template>
