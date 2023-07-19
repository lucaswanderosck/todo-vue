<script setup>
const props = defineProps([
  "registerTask",
  "tempTask",
  "changeFilter",
  "editTempTask",
]);
</script>

<template>
  <form @submit.prevent="props.registerTask">
    <div class="row">
      <div class="col">
        <input
          :value="props.tempTask"
          @change="props.editTempTask"
          type="text"
          placeholder="Digite aqui a descrição da tarefa"
          class="form-control"
          required
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">cadastrar</button>
      </div>
      <div class="col-md-2">
        <select class="form-control" @change="props.changeFilter">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
