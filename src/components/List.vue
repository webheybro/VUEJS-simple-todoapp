<template>
  <div class="list">
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <button @click="editTodo(todo)">Edit</button>
        <button @click="deleteTodo(todo)">Delete</button>
        <span v-if="todoToEdit !== null && todoToEdit.id === todo.id">
          <input
            type="text"
            v-model="todoToEdit.name"
            @keypress.enter="updateTodo"
          />
          <button @click="updateTodo">update</button>
        </span>
        <span v-else>{{ todo.name }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  emits: ["delete-todo", "edit-todo"],
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    let deleteTodo = (todo) => emit("delete-todo", todo);

    let todoToEdit = ref(null);

    let editTodo =  (todo) => todoToEdit.value = todo;
    let updateTodo = function () {
      emit("edit-todo", todoToEdit.value);
      todoToEdit.value = null;
    };

    return { deleteTodo, editTodo, updateTodo, todoToEdit };
  },
};
</script>

<style>
.list {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>