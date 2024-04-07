<template>
  <div class="custom-modal" v-if="openModal">
    <div class="custom-modal-dialog">
      <form @submit.prevent="saveTask()">
        <div class="custom-modal-content">
          <div class="custom-modal-header">
            <h5 class="custom-modal-title">{{ modalTitle }}</h5>
          </div>
          <div class="custom-modal-body">
            <input
              type="text"
              class="form-control mb-1"
              placeholder="task title goes here"
              v-model="task.title"
            />
            <input
              type="text"
              class="form-control mb-1"
              v-model="task.subtitle"
              placeholder="sub-title"
            />
            <textarea
              rows="5"
              class="form-control mb-1"
              v-model="task.description"
              placeholder="Description"
            ></textarea>
            <div
              class="input-group mb-1"
              v-for="(subtask, index) in task.subtasks"
              :key="index"
            >
              <input
                type="text"
                class="form-control"
                v-model="task.subtasks[index].item"
                :placeholder="'Subtask ' + (index + 1)"
              />
              <button
                class="btn btn-primary"
                type="button"
                style="font-weight: bold"
                @click="addSubtask"
                v-if="index === task.subtasks.length - 1"
              >
                +
              </button>
              <button
                class="btn btn-danger"
                type="button"
                @click="removeSubtask(index)"
                v-if="index !== task.subtasks.length - 1"
              >
                -
              </button>
            </div>
            <div class="priorSelector">
              <label>Select Task Priority:</label>
              <select
                class="form-select mb-1"
                v-model="task.priority"
                style="font-weight: bold"
              >
                <option value="low">Low</option>
                <option value="medium">Medium</option>
                <option value="high">High</option>
              </select>
            </div>
          </div>
          <div class="custom-modal-footer">
            <button type="submit" class="btn btn-primary">Save changes</button>
            <button type="button" class="btn btn-secondary" @click="closeModal">
              Close
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "TaskForm",
  props: {
    openModal: {
      type: Boolean,
      required: false,
    },
    initialTask: {
      type: Object,
      required: false,
    },
  },
  data() {
    return {
      task: {
        id: "",
        title: "",
        subtitle: "",
        description: "",
        subtasks: [{ item: "", done: false }],
        priority: "low",
        done: false,
      },
    };
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
    saveTask() {
      if (this.task.id) {
        this.$emit("newTask", this.task);
      } else {
        this.task.id = Date.now();
        this.$emit("newTask", this.task);
      }
      this.closeModalAndReset();
    },
    closeModalAndReset() {
      this.closeModal();
      this.resetFields();
    },
    resetFields() {
      this.task.id = "";  
      this.task.title = "";
      this.task.subtitle = "";
      this.task.description = "";
      this.task.priority = "low";
      this.task.subtasks = [{ item: "", done: false }];
    },
    addSubtask() {
      this.task.subtasks.push({ item: "", done: false });
    },
    removeSubtask(index) {
      this.task.subtasks.splice(index, 1);
    },
  },
  watch: {
    initialTask: {
      deep: true,
      immediate: true,
      handler(newValue) {
        if (newValue && Object.keys(newValue).length > 0) {
          this.task = JSON.parse(JSON.stringify(newValue));
        } else {
          this.resetFields();
        }
      },
    },
  },
  computed: {
    modalTitle() {
      return Object.keys(this.initialTask).length > 0
        ? "Editing a Task:"
        : "Create a New Task:";
    },
  },
});
</script>

<style scoped>
.custom-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.custom-modal-dialog {
  background-color: rgb(173, 175, 174);
  border-radius: 5px;
  max-width: 500px;
  width: 100%;
}

.custom-modal-content {
  padding: 20px;
}

.custom-modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #ddd;
  padding-bottom: 10px;
  margin-bottom: 10px;
}

.custom-modal-title {
  color: black;
  margin: 0;
}

.custom-modal-body {
  color: black;
  padding: 20px 0;
}

.custom-modal-footer {
  display: flex;
  justify-content: flex-end;
  border-top: 1px solid #ddd;
  padding-top: 10px;
  margin-top: 10px;
}

.custom-modal-footer button {
  margin-left: 10px;
}
.priorSelector {
  display: flex;
  align-items: center;
  justify-content: center;
}

.priorSelector label {
  margin-right: 1rem;
}
</style>
