<script setup>
import OneTodo from "./OneTodo.vue";

defineProps({
  todos: Array,
});
</script>

<template>
  <ul>
    <OneTodo v-for="todo of todos" :key="todo.id" :todo="todo" />
  </ul>
</template>

<style lang="scss" scoped>
@use "../assets/base.scss" as *;

ul {
  margin-left: 20%;
  width: 60%;
}
</style>
