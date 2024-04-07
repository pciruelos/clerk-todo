<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container">
      <div class="navbar-brand">Cleark To Do Task</div>
      <ul class="navbar-nav">
        <li class="nav-item">
          <button
            class="nav-link"
            @click="openFormModal()"
            style="font-weight: bold"
          >
            CREATE TASK +
          </button>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
  methods: {
    openFormModal() {
      this.$emit("openTaskForm");
    },
  },
};
</script>
