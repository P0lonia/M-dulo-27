<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import Tarefas from './components/Tarefas.vue';


  const estado = reactive({

    filtro: 'todas',
    tarefaTemp: '',

    tarefas: [
      {
        titulo: 'Estudar ES5',
        finalizado: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizado: false,
      },
      {
        titulo: 'Ir para a academia',
        finalizado: true,
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizado === false)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizado === true)
  }
  
  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch ( filtro ) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizado: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <Tarefas :tarefas="getTarefasFiltradas()" :tarefas-b="getTarefasFiltradas().length"/>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
