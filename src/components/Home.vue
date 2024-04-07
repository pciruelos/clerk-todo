<template>
  <NavBar @openTaskForm="createTask()" />
  <div class="container p-5">
    <div class="d-flex justify-content-center align-items-center pb-5">
      <div class="card text-white bg-primary" style="width: 50%">
        <div class="card-body">
          <h2 class="card-title">Welcome!</h2>
          <p class="card-text">Thank you for using our application.</p>
        </div>
      </div>
    </div>
    <TaskList
      :taskList="tasks"
      @taskStatusChanged="updateTasksList"
      @taskDeleted="updateTasksList"
      @taskForEdit="editTask"
    />
    <TaskForm
      :openModal="showModal"
      @close="hideModal"
      @newTask="addTask"
      :initialTask="taskToEdit"
    />
  </div>
</template>

<script>
import TaskList from "./TaskList.vue";
import TaskForm from "./modals/TaskForm.vue";
import NavBar from "./NavBar.vue";

export default {
  name: "HomePage",
  components: {
    NavBar,
    TaskList,
    TaskForm,
  },
  data() {
    return {
      tasks: [],
      showModal: false,
      taskToEdit: "",
    };
  },
  created() {
    this.loadTasks();
  },
  methods: {
    addTask(newTask) {
      const index = this.tasks.findIndex((t) => t.id === newTask.id);
      if (index !== -1) {
        this.tasks[index] = newTask;
      } else {
        this.tasks.push(newTask);
      }
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
      this.loadTasks();
    },
    updateTasksList(updatedTaskList) {
      this.tasks = updatedTaskList;
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    loadTasks() {
      const storedTasks = localStorage.getItem("tasks");
      if (storedTasks) {
        this.tasks = JSON.parse(storedTasks);
      }
    },
    createTask() {
      this.showModal = true;
      this.taskToEdit = {};
    },
    hideModal() {
      this.showModal = false;
    },
    editTask(task) {
      this.showModal = true;
      this.taskToEdit = task;
    },
  },
};
</script>
