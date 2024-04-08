<template>
  <div class="card-container">
    <div
      :class="getBorderClass(task.priority)"
      class="card mb-3"
      v-for="(task, index) in taskList"
      :key="index"
      style="min-width: 300px; max-width: 350px"
    >
      <div
        class="card-header d-flex justify-content-between align-items-center"
      >
        <span>{{ task.subtitle }}</span>
        <span v-if="task.done" class="badge bg-success" style="font-size: 15px"
          >DONE</span
        >
      </div>
      <div class="card-body">
        <h4 class="card-title" style="color: white">{{ task.title }}</h4>
        <p class="card-text">{{ task.description }}</p>
        <div
          v-if="
            task.subtasks &&
            task.subtasks.some((subtask) => subtask.item.trim())
          "
        >
          <h6 class="card-text" style="text-decoration: underline">
            Sub-tasks:
          </h6>
          <div
            v-for="(subtask, subIndex) in task.subtasks"
            :key="subIndex"
            class="form-check"
          >
            <input
              class="form-check-input"
              type="checkbox"
              :id="'subtask-' + subIndex"
              :checked="subtask.done"
              @click="toggleState(subtask)"
            />
            <label
              class="form-check-label"
              :class="{ completed: subtask.done }"
              :for="'subtask-' + subIndex"
              >{{ subtask.item }}</label
            >
          </div>
        </div>
        <div class="footerBtn">
          <button
            type="button"
            class="btn btn-sm"
            :class="{ 'btn-info': !task.done, 'btn-outline-info': task.done }"
            @click="toggleState(task)"
          >
            {{ task.done ? "Undo" : "Done" }}
          </button>
          <button
            type="button"
            class="btn btn-sm btn-danger"
            @click="deleteTask(index)"
          >
            Delete
          </button>
          <button
            type="button"
            class="btn btn-sm btn-warning"
            @click="editTask(task)"
          >
            Edit
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "TaskList",
  props: {
    taskList: {
      type: Array,
      required: false,
    },
  },
  data() {
    return {
      updatedTaskList: [],
      showModal: false,
    };
  },
  methods: {
    getBorderClass(priority) {
      switch (priority) {
        case (priority = "low"):
          return "border-primary";
        case (priority = "medium"):
          return "border-warning";
        case (priority = "high"):
          return "border-danger";
        default:
          return "";
      }
    },
    deleteTask(index) {
      this.updatedTaskList = this.taskList;
      this.updatedTaskList.splice(index, 1);
      alert("task has been deleted");
      this.$emit("taskDeleted", this.updatedTaskList);
    },
    toggleState(item) {
      item.done = !item.done;
      this.updatedTaskList = this.taskList;
      this.$emit("taskStatusChanged", this.updatedTaskList);
    },
    editTask(task) {
      this.$emit("taskForEdit", task);
    },
    hideModal() {
      this.showModal = false;
    },
  },
});
</script>

<style scoped>
.card-container {
  column-count: 4;
  column-gap: 20px;
  width: 100%;
}
.card {
  display: inline-block;
  width: 100%;
  margin-bottom: 20px;
  break-inside: avoid;
}
.completed {
  text-decoration: line-through !important;
}
.taskCompleteClass {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 10px;
  padding-bottom: 10px;
}
.customCenter {
  margin: 0;
}
.paddingTextComplete {
  padding-left: 5px;
}
.footerBtn {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  padding-top: 15px;
}
</style>
