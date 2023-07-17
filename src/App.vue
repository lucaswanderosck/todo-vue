<script setup>
import { reactive } from "vue";

const estado = reactive({
  tarefaTemp: "",
  filtro: "todas",
  tarefas: [
    {
      titulo: "Estudar SASS",
      finalizada: false,
    },
    {
      titulo: "Estudar Vue",
      finalizada: false,
    },
    {
      titulo: "Ir á academia",
      finalizada: true,
    },
  ],
});

const getTasks = () => {
  return estado.tarefas.filter((tarefa) => !tarefa.finalizada);
};

const getTasksEnds = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada);
};

const getFilterTasks = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTasks();
    case "finalizadas":
      return getTasksEnds();
    default:
      return estado.tarefas;
  }
};

const cadastraTask = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };

  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = "";
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ getTasks().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastraTask">
      <div class="row">
        <div class="col">
          <input
            :value="estado.tarefaTemp"
            required
            @change="(evento) => (estado.tarefaTemp = evento.target.value)"
            type="text"
            placeholder="Digite aqui a descrição da tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">cadastrar</button>
        </div>
        <div class="col-md-2">
          <select
            class="form-control"
            @change="(evento) => (estado.filtro = evento.target.value)"
          >
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="mt-4 list-group">
      <li class="list-group-item" v-for="tarefa in getFilterTasks()">
        <input
          @change="(evento) => (tarefa.finalizada = evento.target.checked)"
          :checked="tarefa.finalizada"
          :id="tarefa.titulo"
          type="checkbox"
        />
        <label
          :class="{ done: tarefa.finalizada }"
          :for="tarefa.titulo"
          class="ms-3"
          >{{ tarefa.titulo }}</label
        >
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
