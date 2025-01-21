<script setup>
import { reactive } from "vue";
import AddTodo from "./components/AddTodo.vue";

let todos = reactive([]);

async function addOneTodo(newTodo) {
  console.log(newTodo);
  try {
    await fetch("http://localhost:5000/addTodo", {
      method: "POST",
      body: JSON.stringify({
        name: newTodo,
        done: 0,
      }),
      headers: {
        "Content-Type": "application/json",
      },
    });
  } catch (error) {
    console.log(error);
  }
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
