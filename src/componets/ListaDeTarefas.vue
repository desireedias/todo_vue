<script setup>
const props = defineProps([
    'tarefas',
])
</script>

<template>
    <ul v-if="props.tarefas.length > 0" class="list-group mt-4" >
        <!-- Bloco de iteração -->
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefas.titulo">
            <!-- Checkbox -->
            <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado"
                :id="tarefa.titulo" type="checkbox">
            <!-- Label -->
            <label :class="{ done: tarefa.finalizado }" class="ms-2" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
        </li>
    </ul>
    <p v-else class="mensagem-vazia">
        Não possui tarefas pendentes!
    </p>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}

.mensagem-vazia{
    margin-top: 15px;
    padding: 15px;
    background-color: #f0f0f0;
    border-radius: 5px;
    text-align: center;
    color: #555;
    font-weight: bold;
}
</style>