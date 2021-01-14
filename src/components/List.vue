<template>
  <div class="list">
    <ul>
      <li v-for="tech in technos" :key="tech.id">
        <button @click="editTechno(tech)">Edit</button>
        <button @click="deleteTechno(tech)">Delete</button>
        <span v-if="technoToEdit !== null && technoToEdit.id === tech.id">
          <input
            type="text"
            v-model="technoToEdit.name"
            @keypress.enter="updateTechno"
          />
          <button @click="updateTechno">update</button>
        </span>
        <span v-else>{{ tech.name }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  emits: ["delete-techno", "edit-techno"],
  props: {
    technos: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    let deleteTechno = (tech) => emit("delete-techno", tech);

    let technoToEdit = ref(null);
    let editTechno = function (tech) {
      technoToEdit.value = tech;
    };
    let updateTechno = function () {
      emit("edit-techno", technoToEdit.value);
      technoToEdit.value = null;
    };

    return { deleteTechno, editTechno, updateTechno, technoToEdit };
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