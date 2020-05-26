<template>
	<div class="options">
		<h2>Choose a base currency: </h2>
		<!-- Extra div to make the absolute position of the lang_options div relative to it-->
		<div id="">
			<div v-on:click="changeList" v-bind:style="styleList" id="lang_options" >
				<div class = "arrow" ></div>
				<p id = "lang_selected" title="Linguagem">{{currencySelected}}</p> 
				<div class="list-group" v-for="(currency, index) in currencies" v-bind:key="index">
					<p class = "lang_item" v-bind:id='currency' v-on:click="selectCurrency(currency)">{{currency}}</p>
				</div>
			</div>
		</div>
		<input type="text" v-model='generalCurrency_value' v-bind:placeholder='currencySelected'>
		<div id="Converters">
			<div class="linha">
				<Converter v-bind:currency-a='currencySelected' currency-b="USD" v-bind:general-currency-value='generalCurrency_value'/>
				<Converter v-bind:currency-a='currencySelected' currency-b="EUR" v-bind:general-currency-value='generalCurrency_value'/>
				<Converter v-bind:currency-a='currencySelected' currency-b="CAD" v-bind:general-currency-value='generalCurrency_value'/>
			</div>
			<div class="linha">
				<Converter currency-a="USD" v-bind:currency-b='currencySelected' general-currency-value='0'/>
				<Converter currency-a="EUR" v-bind:currency-b='currencySelected' general-currency-value='0'/>
				<Converter currency-a="CAD" v-bind:currency-b='currencySelected' general-currency-value='0'/>
			</div>
		</div>
	</div>
          
</template>


<script >
	import Converter from './Converter.vue'
	
	export default{
		name: 'Options',
		components:{
			Converter
		},
		data(){
			return{
				currencyList:[],
				styleList: {height: '29px'},
				currencySelected: 'BRL',
				generalCurrency_value: ''
			}
		},
		methods:{
			changeList(){
				
				//URL to the currency converter
				let url = 'https://api.exchangeratesapi.io/latest';

				/*fetch sends a GET request to the URL above. It receives a response that
				is converted to JSON and then all its properties names are converted into
				an array*/
				fetch(url).then(res => res.json()).then(json => { 
					this.currencyList = Object.getOwnPropertyNames(json.rates);
				});

				//Small arrow in the dropdown list
				var arrow = document.querySelector(".arrow");

				/*If the dropdown list is in its "smaller mode" then it gets in its "bigger
				mode" while the arrow rotates and change a little its hight*/
				if(this.styleList.height == "29px"){
					this.styleList.height = "493px";
					arrow.style.transform = "rotate(-135deg)";
					arrow.style.top = "10px";
				}

				//If the dropdown list is in its "bigger mode" the opposite happens
				else{
					this.styleList.height = "29px";
					arrow.style.transform = "rotate(45deg)";
					arrow.style.top = "7px";
				}
				
			},

			//currencySelected is set to be the currency (in a p tag) that the user has clicked
			selectCurrency(c){
				this.currencySelected = c;

			}
		},
		computed:{
			currencies(){
				return this.currencyList;
			}
		}
	}




</script>


<style scoped>
	.options{
		margin-bottom: 100px;
	}
	h2{
		text-align:center;
		margin: 0;
	}

	#lang_options{
		width: 85px;
		border: 0px;
		display: inline-block; 
		margin-top: 40px;
		background-color: white;
		color: var(--titlesColor);
		border-radius: 20px;
		position: absolute;
		font-family: Arial, sans-serif;
		font-weight: 600;
		font-size: 16px;
		cursor: pointer;
		transition: all 300ms ease-out;
		box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
		height: 29px;   
		overflow-y: hidden; 
		left: 0;
		right: 0;
		margin-left: auto;
		margin-right: auto;
	}

	#lang_options p{
		margin: 0px;
		padding-top: 5px;
		padding-bottom: 5px;
		padding-right: 10px;
	}


	.lang_item:hover{
		background-color: #d9d9d9;
	}

	.arrow {
		border: solid black;
		border-width: 0 3px 3px 0;
		display: inline-block;
		padding: 3px;
		transform: rotate(45deg);
		position: absolute;
		left: 71%;
		top: 7px;
		transition: all 300ms ease-out;
	}	

	#Converters{
		margin-top: 60px;
	}

	.linha{
		display: flex;
		justify-content: space-evenly;
		margin-bottom: 30px;
	}

</style>