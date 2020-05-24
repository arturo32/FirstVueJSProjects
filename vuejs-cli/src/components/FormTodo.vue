<template>
	<div class="form-todo form-group"> 
			
			<p>
				<input  placeholder = "Name" type="text" name="author" class="form-control" v-model="name">
			</p>

			<p>
				<textarea placeholder="Comment" name="message" class="form-control" v-model="message"></textarea>
			</p>
			
			<button v-on:click="addComment" type="submit" class="btn btn-primary">Comment</button>
		</div>
</template>

<script type="text/javascript">
	export default{
		data(){
			return{
				name: "",
				message: ""
			}
		},
		methods: {
			addComment(){
				if(this.message.trim() == "") return;

				//Emiting event for the Comments.vue listen
				this.$emit('add-todo', {
					name: this.name,
					message: this.message
				})

				this.name = "";
				this.message = "";
			}
		}
	}
</script>