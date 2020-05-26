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
			//Convert the currencyA to currencyB
			convert(){
				//cA is the value to be converted. If the user didn't put anything it becomes zero       
				let cA = this.currencyA_value? this.currencyA_value:0; 

				//URL to the currency converter
				let url = 'https://api.exchangeratesapi.io/latest?base=' + this.currencyA + '&symbols=' + this.currencyB;
				
				/*fetch sends a GET request to the URL above. It receives a response that
				is converted to JSON and then the exchange rate (er) is collected from 
				the object and used to calculated the final converted value*/
				fetch(url).then(res => res.json()).then(json => {
					let er = json.rates[this.currencyB];
					this.currencyB_value = (er * parseFloat(cA)).toFixed(2);

				});
			}
			
		},
		watch: {

			/*If generalCurrencyValue changes to a non-zero value then currencyA_value
			is set to be this value*/
			generalCurrencyValue: function(a){
				if(a != 0){
					this.currencyA_value = this.generalCurrencyValue;
					this.convert();
				}
			},
			
			//If currencyA changes the convert function is called again
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



