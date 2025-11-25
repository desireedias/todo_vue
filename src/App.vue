<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './componets/Cabecalho.vue';
  import Formulario from './componets/Formulario.vue';
  import ListaDeTarefas from './componets/ListaDeTarefas.vue';

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" v-model="estado.tarefaTemp" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
    
  </div>
</template>


