<script setup>
    import { reactive } from 'vue';
    import Cabecalho from './components/Cabecalho.vue'
    import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue';
    // import ListaDeTarefas from './components'

const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
        {
            titulo: 'Estudar Python',
            finalizada: false,

        },
        {
            titulo: 'Ir ao mercado as 15hrs',
            finalizada: false,

        },
        {
            titulo: 'Caminhar',
            finalizada: true,

        }
    ]
})

const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
    const { filtro } = estado;

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
    const tarefaNova = {
        titulo: estado.tarefaTemp,
        finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
}

</script>

<template>
    <div class="container">
     <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"/>
     <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarfa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
     <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
    </div>
    
   
</template>


