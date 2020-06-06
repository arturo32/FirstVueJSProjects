<template>
	<div>
		<h3>Todos</h3>
		<div class="legend">
			<span>Double click to mark as complete</span>
			<span>
				<span class="incomplete-box"></span> = Incomplete
			</span>
			<span>
				<span class="complete-box"></span> = Complete
			</span>
		</div>
		<div class="todos">
			<div 
				v-for="todo in allTodos" 
				v-bind:class="{'is-complete':todo.completed}"
				v-on:dblclick="onDblClick(todo)" 
				v-bind:key="todo.id" class="todo">
				{{todo.title}}
				<div v-on:click="deleteTodo(todo.id)" class="delete"><i class="fa fa-times-rectangle"></i></div>
			</div>
		</div>
	</div>
</template>

<script>
	import { mapGetters, mapActions } from 'vuex';

	export default{
		name: "Todos",
		methods: { 
			...mapActions(["fetchTodos", "deleteTodo", "updateTodo"]),
			onDblClick(todo){
				const updTodo = {
					id: todo.id,
					title: todo.title,
					completed: !todo.completed
				}
				this.updateTodo(updTodo);
			}
		},
		computed: mapGetters(['allTodos']),
		created() { 
			this.fetchTodos();
		}
	};
</script>

<style scoped>
	.todos {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-gap: 1rem;
	}
	.todo {
		border: 1px solid #ccc;
		background: #41b883;
		padding: 1rem;
		border-radius: 5px;
		text-align: center;
		position: relative;
		cursor: pointer;
		user-select: none;	
	}
	.delete{
		color: white;
		display: inline-block;
		position: absolute;
		bottom: 0px;
		right: 7px;
	}

	.delete i{
		font-size: 19px;
	}
	.legend {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		margin-bottom: 1rem;
		grid-column-gap: 20px;
	}

	.complete-box {
		display: inline-block;
		width: 10px;
		height: 10px;
		background: #35495e;
	}
	.incomplete-box {
		display: inline-block;
		width: 10px;
		height: 10px;
		background: #41b883;
	}

	.is-complete {
		background: #35495e;
		color: #fff;
	}

	@media (max-width: 500px){
		.todos{
			grid-template-columns: 1fr;
		}
		.legend{
			grid-template-columns: 1fr;
		}
	}

</style>