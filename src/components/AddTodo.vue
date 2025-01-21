<script setup>
import { toTypedSchema } from "@vee-validate/zod";
import { useField, useForm } from "vee-validate";
import { ref } from "vue";
import { z } from "zod";

const props = defineProps({
  todos: Array,
});

const emit = defineEmits(["addOneTodo"]);

const sameTodo = ref(false);

const schema = z.object({
  todo: z
    .string({ message: "ce champ est requis" })
    .min(3, { message: "Trop court !" }),
});

const { handleSubmit, resetForm } = useForm({
  validationSchema: toTypedSchema(schema),
});

const { value: todoValue, errorMessage: todoError } = useField("todo", {
  validateOnValueUpdate: false,
});

const submit = handleSubmit((values) => {
  //   console.log(values);
  sameTodo.value = false;
  const alreadyExists = props.todos.find(
    (oneTodo) => oneTodo.name.toLowerCase() === values.todo.toLowerCase()
  );
  console.log(alreadyExists);
  if (!alreadyExists) {
    emit("addOneTodo", values.todo);
    resetForm();
  } else {
    sameTodo.value = true;
  }
});
</script>

<template>
  <form class="m-20 d-flex justify-content-center" @submit="submit">
    <div class="d-flex flex-column">
      <input type="text" class="sameHeight mr-10 mb-10" v-model="todoValue" />
      <p v-if="todoError">{{ todoError }}</p>
      <p v-if="sameTodo">Todo déjà existante</p>
    </div>
    <button class="btn btn-primary sameHeight">Submit</button>
  </form>
</template>

<style lang="scss" scoped>
@use "../assets/base.scss" as *;

input {
  width: 300px;
}

p {
  color: red;
}

.sameHeight {
  height: 40px;
}
</style>
