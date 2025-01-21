<script setup>
import { onMounted, reactive } from "vue";
import AddTodo from "./components/AddTodo.vue";
import TodoList from "./components/TodoList.vue";

let todos = reactive([]);

async function getTodos() {
  const allTodos = await fetch("http://localhost:5000");
  const response = await allTodos.json();
  console.log(response);
  todos.splice(0, todos.length, ...response);
}

onMounted(() => {
  getTodos();
});

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
    await getTodos();
  } catch (error) {
    console.log(error);
  }
}

async function deleteTodo(todoId) {
  console.log(todoId);

  try {
    await fetch(`http://localhost:5000/deleteTodo/${todoId}`, {
      method: "DELETE",
    });
    await getTodos();
  } catch (error) {
    console.log(error);
  }
}

async function toggleTodo(todo) {
  // console.log(todo);
  try {
    await fetch("http://localhost:5000/toggleTodo", {
      method: "PATCH",
      body: JSON.stringify(todo),
      headers: {
        "Content-Type": "application/json",
      },
    });
    await getTodos();
  } catch (error) {
    console.log(error);
  }
}
</script>

<template>
  <div class="app-container">
    <AddTodo @add-one-todo="addOneTodo" :todos="todos" />
    <TodoList
      :todos="todos"
      @delete-todo="deleteTodo"
      @toggle-todo="toggleTodo"
    />
  </div>
</template>

<style lang="scss">
@use "./assets/base.scss" as *;

.app-container {
  min-height: 100vh;
}
</style>
