<template>
  <div id="app">
    <h1>Todos list</h1>
    <Form @add="saveTodos" />
    <br />
    <List
      :todos="todos"
      @delete-todo="deleteTodos"
      @edit-todo="editTodos"
    />
  </div>
</template>

<script>
import Form from "@/components/Form";
import List from "@/components/List";
import { ref } from "vue"; //equivalent useState

export default {
  name: "App",
  components: { Form, List },
  setup() {
    let todos = ref([]);
    const saveTodos = function (data) {
      todos.value = [...todos.value, { name: data, id: Date.now() }];
    };

    const editTodos = function (tech) {
      todos.value = todos.value.map((item) =>
        item?.id === tech.id ? tech : item
      );
    };

    const deleteTodos = function (tech) {
      todos.value = todos.value.filter((item) => item?.id !== tech.id);
    };

    return { saveTodos, editTodos, deleteTodos, todos };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul {
  list-style: none;
  text-align: left;
  margin-left: 0;
  padding-left: 0;
}
</style>
