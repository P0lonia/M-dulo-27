<script setup>
    const props = defineProps(['tarefas', 'tarefasB'])
</script>

<template>
    <ul v-if="tarefasB > 0" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizado }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <h3 class="mt-5 d-flex justify-content-center" v-else>Não há tarefas...</h3>
</template>