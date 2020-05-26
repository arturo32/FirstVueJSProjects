<template>
	<div class="converter">
		<h3>{{currencyA}} to {{currencyB}}</h3>
		<input type="text" v-model='currencyA_value' v-on:input="convert" v-bind:placeholder="currencyA">
		<h3>{{currencyB_value}}</h3>

	</div>
</template>

<script>
	export default{
		name: 'Converter',
		props: ['currencyA', 'currencyB', 'generalCurrencyValue'],
		data(){
			return{
				currencyA_value: '',
				currencyB_value: parseFloat(0).toFixed(2)
			}
		},
		methods: {
			convert(){
				let cA = this.currencyA_value? this.currencyA_value:0; 
				let url = 'https://api.exchangeratesapi.io/latest?base=' + this.currencyA + '&symbols=' + this.currencyB;
				
				fetch(url).then(res => res.json()).then(json => {
					console.log(json);
				let price = json.rates[this.currencyB];
				this.currencyB_value = (price * parseFloat(cA)).toFixed(2);

				})
			}
			
		},
		watch: {
			generalCurrencyValue: function(a){
				if(a != 0){
					this.currencyA_value = this.generalCurrencyValue;
					this.convert();
				}
			},
			currencyA: function(){
				if(this.currencyA_value){
					this.convert();
				}
			}
		}
		
		

	}
</script>


<style scoped>
	.converter{
		max-width: 300px;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
		padding: 17px;
		height: 150px;
	}

	.button{
		margin-top:10px;

	}
</style>



