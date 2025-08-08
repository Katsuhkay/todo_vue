<script setup>
const props = defineProps(['tarefas'])
</script>

<template>
	<!-- Lista visível se houver pelo menos uma tarefa -->
	<ul v-if="tarefas.length > 0" class="list-group mt-4">
		<li
			class="list-group-item"
			v-for="tarefa in tarefas"
			:key="tarefa.titulo"
		>
			<input
				@change="(evento) => (tarefa.finalizada = evento.target.checked)"
				:checked="tarefa.finalizada"
				:id="tarefa.titulo"
				type="checkbox"
			/>
			<label
				:class="{ done: tarefa.finalizada }"
				class="ms-3"
				:for="tarefa.titulo"
			>
				{{ tarefa.titulo }}
			</label>
		</li>
	</ul>

	<!-- Se não houver tarefas -->
	<p v-else class="mt-4 text-muted">Nenhuma tarefa encontrada.</p>

	<!-- Se todas as tarefas estiverem concluídas -->
	<p
		v-if="tarefas.length > 0 && tarefas.every(tarefa => tarefa.finalizada)"
		class="mt-3 alert alert-success"
	>
		Todas as tarefas concluídas!
	</p>
</template>

<style scoped>
.done {
	text-decoration: line-through;
}
</style>
