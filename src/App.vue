<script setup>
import { reactive } from "vue";
import AddTodo from "./components/AddTodo.vue";

let todos = reactive([]);

function addOneTodo(newTodo) {
  console.log(newTodo);
  // requete http
}
</script>

<template>
  <div class="app-container">
    <AddTodo @add-one-todo="addOneTodo" />
  </div>
</template>

<style lang="scss">
@use "./assets/base.scss" as *;

.app-container {
  min-height: 100vh;
}
</style>
