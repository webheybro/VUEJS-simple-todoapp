<template>
  <form @submit.prevent="addTodo">
    <input type="text" name="newTodo" v-model="newTodo" />
    <br />
    <button type="submit">Ajouter</button>
  </form>
</template>

<script>
import { ref } from "vue";
export default {
  setup(props, ctx) {
    let newTodo = ref("");
    const addTodo = function () {
      ctx.emit("add", newTodo.value);
      newTodo.value = "";
    };
    return { newTodo, addTodo};
  },
};
</script>

<style>
</style>