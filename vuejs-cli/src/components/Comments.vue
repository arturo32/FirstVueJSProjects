<template>
	<div class="container">
		<h1>Commments</h1>
		<hr>
		
		<FormTodo v-on:add-todo="addComment"> </FormTodo>

		<div class="list-group">
			<p v-if="comments.length == 0">No comments</p>
			<div class="list-group-item" v-for="(c, index) in allComents" v-bind:key="index">
				<span class="comment_author">Author: <strong>{{c.name}}</strong></span>
				<p>{{c.message}}</p>
				<div>
					
					<a v-on:click.prevent="deleteComment(index)" href="" title="Delete" >Delete</a>				
				</div>
			</div>
		</div>

	</div>
</template>

<script type="text/javascript">
	import FormTodo from './FormTodo';
	export default{
		components: {
			FormTodo
		},
		data(){
			return{
				comments: []
			}
		},
		methods: {
			addComment(c){
				this.comments.push(c);
			},
			deleteComment(index){
				this.comments.splice(index, 1);
			}

		},
		computed: {
			allComents(){
				return this.comments.map(c => ({...c, name: c.name.trim() == ""? "Anonymous" : c.name })  );
			}
		},
		watch: {
			comments(val){
				console.log("value: ", val);
			}
		}
	}
</script>