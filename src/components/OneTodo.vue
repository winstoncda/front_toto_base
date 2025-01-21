<script setup>
defineProps({
  todo: Object,
});

const emit = defineEmits(["deleteTodo", "toggleTodo"]);
</script>

<template>
  <div class="mb-20 d-flex align-items-center p-10">
    <p class="flex-fill">
      {{ todo.name }} <span v-if="todo.done">&#x2713;</span>
    </p>
    <button @click="emit('toggleTodo', todo)" class="btn btn-success mr-10">
      <span v-if="!todo.done">Check</span>
      <span v-if="todo.done">Cancel</span>
    </button>
    <button @click="emit('deleteTodo', todo.id)" class="btn btn-danger">
      Delete
    </button>
  </div>
</template>

<style lang="scss" scoped>
@use "../assets/base.scss" as *;

div {
  border: var(--border);
  background-color: white;
  p {
    font-weight: 700;
    span {
      margin-left: 10px;
      color: green;
    }
  }
}
</style>
