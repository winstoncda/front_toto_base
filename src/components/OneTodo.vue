<script setup>
defineProps({
  todo: Object,
});

const emit = defineEmits(["deleteTodo", "toggleTodo"]);
</script>

<template>
  <div class="mb-20 d-flex align-items-center p-10">
    <p class="flex-fill">{{ todo.name }}</p>
    <button @click="emit('toggleTodo', todo)" class="btn btn-success mr-10">
      Check
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
  }
}
</style>
