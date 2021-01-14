<template>
  <div>
    <h1>Veille techno</h1>
    <Form @add="saveTechno" />
    <br />
    <List
      :technos="technos"
      @delete-techno="deleteTechno"
      @edit-techno="editTechno"
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
    let technos = ref([]);
    const saveTechno = function (data) {
      technos.value = [...technos.value, { name: data, id: Date.now() }];
    };

    const editTechno = function (tech) {
      technos.value = technos.value.map((item) =>
        item.id === tech.id ? tech : item
      );
    };

    const deleteTechno = function (tech) {
      technos.value = technos.value.filter((item) => item.id != tech.id);
    };

    return { saveTechno, editTechno, deleteTechno, technos };
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
  margin-left: 0px;
  padding-left: 0px;
}
</style>
