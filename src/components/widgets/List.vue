<template>
  <h1>{{ message }}</h1>
  <ul>
    <li v-for="task in tasks" :key="task.id">
      <p>{{ task.name }}</p>
      <button class="edit" @click="editItem(task)">Editar</button>
      <button class="delete" @click="deleteItem(task.id)">Eliminar</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "ListItems",
  data() {
    return {
    };
  },
  props: [
    "tasks",
    "message"
  ],
  methods: {
    editItem(task) {
        this.$emit("editTask", task);
    },
    deleteItem(id) {
        this.$emit("deleteTask", id);
    }
  }
};
</script>

<style></style>
