<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: "todas",
  tarefaTemp: '',
  tarefas: [
    {
      titulo: "Estudar ES6",
      finalizado: false,
    },
    {
      titulo: "estudar SASS",
      finalizado: false,
    },
    {
      titulo: "ir para a academia",
      finalizado: true,
    }
  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizado)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizado)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  //1.cria o objeto da nova tarefa
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizado: false,
  }

  //2.adiciona a nova tarefa no array reativo (atualiza a lista na tela)
  estado.tarefas.push(tarefaNova);
  //lógica de limpeza
  estado.tarefaTemp = '';
  
}


</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Voce possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input v-model="estado.tarefaTemp" required type="text" placeholder="Digite aqui sua tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Adicionar Tarefa</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>


    <ul class="list-group mt-4" >
      <!-- Bloco de iteração -->
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <!-- Checkbox -->
        <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
        <!-- Label -->
        <label :class="{done: tarefa.finalizado}" class="ms-2" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
