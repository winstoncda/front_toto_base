<script setup>
defineProps({
  todo: Object,
});
</script>

<template>
  <div class="mb-20 d-flex align-items-center p-10">
    <p class="flex-fill">{{ todo.name }}</p>
    <button class="btn btn-success mr-10">Check</button>
    <button class="btn btn-danger">Delete</button>
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
