<script setup>
import { reactive } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import List from "./components/List.vue";

const state = reactive({
  tempTask: "",
  filter: "todas",
  tasks: [
    {
      title: "Estudar SASS",
      finished: false,
    },
    {
      title: "Estudar Vue",
      finished: false,
    },
    {
      title: "Ir á academia",
      finished: true,
    },
  ],
});

const getTasks = () => {
  return state.tasks.filter((task) => !task.finished);
};

const getTaskFinished = () => {
  return state.tasks.filter((task) => task.finished);
};

const getFilterTasks = () => {
  const { filter } = state;

  switch (filter) {
    case "pendentes":
      return getTasks();
    case "finalizadas":
      return getTaskFinished();
    default:
      return state.tasks;
  }
};

const registerTask = () => {
  const newTask = {
    title: state.tempTask,
    finished: false,
  };

  state.tasks.push(newTask);
  state.tempTask = "";
};
</script>

<template>
  <div class="container">
    <Header :get-tasks="getTasks().length" />
    <Form
      :change-filter="(event) => (state.filter = event.target.value)"
      :temp-task="state.tempTask"
      :edit-temp-task="(event) => (state.tempTask = event.target.value)"
      :register-task="registerTask"
    />
    <List :tasks="getFilterTasks()" />
  </div>
</template>
