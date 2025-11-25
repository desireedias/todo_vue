<script setup>
const props = defineProps([
    'cadastraTarefa',
    'modelValue',
    'tarefaTemp',
    'trocarFiltro',
    'editarTarefaTemp',
    ])

    const emits = defineEmits(['update:modelValue']);
    const eventoInput = (evento) => {
      emits('update:modelValue', evento.target.value);
    };

</script>



<template>
    <form @submit.prevent="props.cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="props.modelValue" @input="eventoInput" required type="text" placeholder="Digite aqui sua tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Adicionar Tarefa</button>
        </div>
        <div class="col-md-2">
          <!-- "evento => estado.filtro = evento.target.value" ESTE TRECHO FOI TROCADO PELO PROPS.TROCARFILTRO -->
          <select @change="props.trocarFiltro" class="form-control">
            <option value="todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
</template>