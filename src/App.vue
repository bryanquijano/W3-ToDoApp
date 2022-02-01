<script setup>
import { ref, computed } from "vue";

// Empty reference
const newTodo = ref("");

const todos = ref([]);

const pending = computed(() => {
  return todos.value.filter((todo) => !todo.done);
});

const completed = computed(() => {
  return todos.value.filter((todo) => todo.done);
});

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: todos.value.length,
      content: newTodo.value,
      done: false,
    });
    newTodo.value = "";
  }
};

const changeStatus = (id) => {
  const todo = todos.value.find((todo) => todo.id == id);
  todo.done = !todo.done;
};
</script>

<template>
  <div class="min-h-screen bg-gray-900">
    <div class="container flex flex-col pt-8 mx-auto space-y-16">
      <h1 class="text-6xl font-medium tracking-tight text-center text-gray-100">
        Bryan's Todo App
      </h1>
      <input
        @change="addTodo"
        v-model="newTodo"
        type="text"
        class="px-4 py-4 text-3xl text-center rounded-full"
        placeholder="Add a new item..."
      />
      <div class="flex justify-around">
        <div class="w-1/3">
          <h3
            class="py-4 text-2xl text-center text-white bg-gray-400 rounded-md"
          >
            Pending
          </h3>
          <ul class="pt-8 space-y-4">
            <li
              v-for="todo in pending"
              :key="todo.id"
              @click="changeStatus(todo.id)"
              class="w-full px-4 py-4 font-bold text-center text-gray-600 duration-200 bg-gray-300 rounded-lg hover:cursor-pointer hover:bg-gray-400 hover:text-gray-200"
            >
              {{ todo.content }}
            </li>
          </ul>
        </div>
        <div class="w-1/3">
          <h3
            class="py-4 text-2xl text-center text-white bg-green-400 rounded-md"
          >
            Completed
          </h3>
          <ul class="pt-8 space-y-4">
            <li
              v-for="todo in completed"
              :key="todo.id"
              @click="changeStatus(todo.id)"
              class="w-full px-4 py-4 font-bold text-center text-white duration-200 bg-green-300 rounded-lg hover:cursor-pointer hover:bg-green-400 hover:text-green-200"
            >
              {{ todo.content }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
