<template>
  <div class="button-wrapper" v-if="!editedTask">
    <input
      class="input-tarea"
      v-model="newTask"
      type="text"
      placeholder="Agregar nueva tarea"
    />
    <button @click="addItem()">Agregar</button>
    <button class="delete" @click="clearItems()">Vaciar lista</button>
  </div>

  <div class="button-wrapper" v-else>
    <input
      class="input-tarea"
      v-model="newTask"
      type="text"
      placeholder="Editar tarea"
    />
    <button @click="updateItem()">Guardar</button>
    <button
      class="cancel"
      @click="cancel()"
    >
      Cancelar
    </button>
  </div>
</template>

<script>
export default {
  name: "ManageList",
  data() {
    return {
      newTask: "",
    };
  },
  props: [
    "editedTask"
  ],
  methods: {
    addItem() {
        this.$emit("addTask", this.newTask);
        this.newTask = "";
    },
    clearItems() {
        this.$emit("clearTasks");
    },
    updateItem(){
        this.$emit("updateTask", this.newTask);
    },
    cancel(){
        this.newTask = "";
        this.$emit("cancelActions");
    }
  }
};
</script>

<style></style>
