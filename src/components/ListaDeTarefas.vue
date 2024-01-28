<script setup>
const props = defineProps(['tarefas']);
</script>

<template>
    <ul v-if="props.tarefas.length > 0" class="list-group mt-4">
        <li v-for="tarefa in props.tarefas" class="list-group-item">
            <input
                @change="e => (tarefa.finalizada = e.target.checked)"
                :checked="tarefa.finalizada"
                type="checkbox"
                :id="tarefa.titulo"
            />
            <label class="ms-3" :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">{{ tarefa.titulo }}</label>
        </li>
    </ul>
    <p v-else class="mt-3 h4">Sem tarefas para exibir</p>
</template>

<style scoped>
.done {
    color: gray;
    text-decoration: line-through;
}
</style>
