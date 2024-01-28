<script setup>
const props = defineProps(['tarefasPendentes']);
</script>

<template>
    <header class="mb-5 mt-5 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>
            Você possui {{ props.tarefasPendentes }}
            {{ props.tarefasPendentes > 1 ? 'tarefas pendentes' : 'tarefa pendente' }}
        </p>
    </header>
</template>
