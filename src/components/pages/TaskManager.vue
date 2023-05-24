<template>
  <div class="taskList">
    <ListItems :tasks="tasks" :message="message" @editTask="editTask($event)"  @deleteTask="deleteTask($event)"></ListItems>
    <ManageList :editedTask="editedTask" @addTask="addTask($event)" @updateTask="updateTask($event)" @clearTasks="clearTasks()" @cancelActions="cancelActions()"></ManageList>
  </div>
</template>

<script>
import ManageList from "../widgets/ManageList.vue";
import ListItems from "../widgets/List.vue";
export default {
  name: "TaskManager",
  components: {
    ManageList,
    ListItems
  },
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
    },
    editTask(task) {
      this.editedTask = task;
      this.newTask = task.name;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    updateTask(event) {
      this.newTask = event;
      const taskIndex = this.tasks.findIndex(
        (task) => task.id === this.editedTask.id
      );
      this.tasks[taskIndex].name = this.newTask;
      this.newTask = "";
      this.editedTask = null;
    },
    addTask(event) {
      this.newTask = event;
      if (this.editedTask) {
        this.updateTask();
      } else {
        const newId = this.tasks.length + 1;
        this.tasks.push({ id: newId, name: this.newTask });
        this.newTask = "";
      }
    },
    cancelActions(){
      this.editedTask = null
    }
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
