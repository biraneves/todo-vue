<script setup>
import { reactive } from 'vue';

const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
        { titulo: 'Estudar ES6', finalizada: false },
        { titulo: 'Estudar SASS', finalizada: false },
        { titulo: 'Estudar JavaScript', finalizada: true },
    ],
});

const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);
};

const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
};

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
};

const cadastraTarefa = () => {
    const tarefaNova = {
        titulo: estado.tarefaTemp,
        finalizada: false,
    };

    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
};
</script>

<template>
    <div class="container">
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Minhas tarefas</h1>
            <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
        </header>
        <form @submit.prevent="cadastraTarefa">
            <div class="row">
                <div class="col">
                    <input
                        :value="estado.tarefaTemp"
                        @change="e => (estado.tarefaTemp = e.target.value)"
                        type="text"
                        placeholder="Descrição da tarefa"
                        class="form-control"
                        required
                    />
                </div>
                <div class="col-md-2">
                    <button type="submit" class="btn btn-primary">Cadastrar</button>
                </div>
                <div class="col-md-2">
                    <select @change="e => (estado.filtro = e.target.value)" class="form-control">
                        <option value="todas">Todas as tarefas</option>
                        <option value="pendentes">Pendentes</option>
                        <option value="finalizadas">Finalizadas</option>
                    </select>
                </div>
            </div>
        </form>
        <ul class="list-group mt-4">
            <li v-for="tarefa in getTarefasFiltradas()" class="list-group-item">
                <input
                    @change="e => (tarefa.finalizada = e.target.checked)"
                    :checked="tarefa.finalizada"
                    type="checkbox"
                    :id="tarefa.titulo"
                />
                <label class="ms-3" :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">{{
                    tarefa.titulo
                }}</label>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.done {
    color: gray;
    text-decoration: line-through;
}
</style>
