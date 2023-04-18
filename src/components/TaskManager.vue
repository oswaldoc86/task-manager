<template>
  <div class="taskList">
    <h1>{{ message }}</h1>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <p>{{ task.name }}</p>
        <button class="edit" @click="editTask(task)">Editar</button>
        <button class="delete" @click="deleteTask(task.id)">Eliminar</button>
      </li>
    </ul>

    <div class="button-wrapper" v-if="!editedTask">
      <input
        class="input-tarea"
        v-model="newTask"
        type="text"
        placeholder="Agregar nueva tarea"
      />
      <button @click="addTask">Agregar</button>
      <button class="delete" @click="clearTasks">Vaciar lista</button>
    </div>

    <div class="button-wrapper" v-else>
      <input
        class="input-tarea"
        v-model="newTask"
        type="text"
        placeholder="Editar tarea"
      />
      <button @click="updateTask">Guardar</button>
      <button
        class="cancel"
        @click="
          editedTask = null;
          newTask = '';
        "
      >
        Cancelar
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskManager",
  data() {
    return {
      message: "Lista de tareas ",
      tasks: [
        { id: 1, name: "Hacer la compra" },
        { id: 2, name: "Ir al gimnasio" },
        { id: 3, name: "Llamar al dentista" },
      ],
      newTask: "",
      editedTask: null,
    };
  },
  methods: {
    clearTasks() {
      this.tasks = [];
      console.log(this.tasks);
    },
    editTask(task) {
      this.editedTask = task;
      this.newTask = task.name;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    updateTask() {
      const taskIndex = this.tasks.findIndex(
        (task) => task.id === this.editedTask.id
      );
      this.tasks[taskIndex].name = this.newTask;
      this.newTask = "";
      this.editedTask = null;
    },
    addTask() {
      if (this.editedTask) {
        this.updateTask();
      } else {
        const newId = this.tasks.length + 1;
        this.tasks.push({ id: newId, name: this.newTask });
        this.newTask = "";
      }
    },
  },
};
</script>

<style>
.taskList {
  font-family: Times New Roman;
  font-size: 1.2rem;
  color: #000000;
  width: 500px;
  margin: 0 auto;
  padding: 2rem 0;
  border: 1px solid #000;
}

.taskList h1 {
  margin-top: 0;
  text-align: center;
}

.taskList ul {
  list-style: none;
  padding: 0;
  margin: 0;
  margin-bottom: 6rem;
}

.taskList li {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  margin-bottom: 0.5rem;
}

.taskList p {
  width: 200px;
  padding: 0.5rem;
  padding-left: 0;
  margin-right: 1rem;
  white-space: normal;
}

.taskList button {
  color: #ffffff;
  border: none;
  padding: 0.5rem;
  margin-left: 1rem;
}

.taskList button:hover {
  cursor: pointer;
}

.taskList button.delete {
  background-color: #f44336;
}

.taskList button.edit {
  background-color: #4caf50;
}

.taskList .button-wrapper {
  text-align: center;
}

.taskList .button-wrapper input {
  width: 200px;
  margin-right: 1rem;
  padding: 0.5rem;
  padding-bottom: 0.5rem;
  border: none;
  border-bottom: 2px solid #000000;
}

.taskList .button-wrapper button {
  background-color: #4caf50;
  color: #ffffff;
  border: none;
  padding: 0.5rem;
  margin-left: 1rem;
}

.taskList .button-wrapper button.delete,
.taskList .button-wrapper button.cancel {
  background-color: #f44336;
}
</style>
