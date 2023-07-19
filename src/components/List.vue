<script setup>
const props = defineProps(["tasks"]);
</script>

<template>
  <ul class="mt-4 list-group">
    <li class="list-group-item" v-for="task in props.tasks">
      <input
        @change="(event) => (task.finished = event.target.checked)"
        :checked="task.finished"
        :id="task.title"
        type="checkbox"
      />
      <label :class="{ done: task.finished }" :for="task.title" class="ms-3">{{ task.title }}</label>
    </li>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
