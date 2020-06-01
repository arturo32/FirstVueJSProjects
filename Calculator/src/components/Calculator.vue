<template>
	<div class="calculator">
		<div class="display">{{currentDisplay}}</div>
		<div class="calculator_key" v-on:click="clear" >C</div>
		<div class="calculator_key" v-on:click="operate('invert')">+/-</div>
		<div class="calculator_key" v-on:click="operate('percent')">%</div>
		<div class="calculator_key" v-on:click="operate('divide')">/</div>
		<div class="calculator_key" v-on:click="append('7')">7</div>
		<div class="calculator_key" v-on:click="append('8')">8</div>
		<div class="calculator_key" v-on:click="append('9')">9</div>
		<div class="calculator_key" v-on:click="operate('multiply')">x</div>
		<div class="calculator_key" v-on:click="append('4')">4</div>
		<div class="calculator_key" v-on:click="append('5')">5</div>
		<div class="calculator_key" v-on:click="append('6')">6</div>
		<div class="calculator_key" v-on:click="operate('subtract')">-</div>
		<div class="calculator_key" v-on:click="append('1')">1</div>
		<div class="calculator_key" v-on:click="append('2')">2</div>
		<div class="calculator_key" v-on:click="append('3')">3</div>
		<div class="calculator_key" v-on:click="operate('add')">+</div>
		<div class="calculator_key zero" v-on:click="append('0')">0</div>
		<div class="calculator_key" v-on:click="operate('dot')">.</div>
		<div class="calculator_key" v-on:click="calculate">=</div>
	</div>
</template>

<script>
export default {
	data() {
		return{
			current: '',
			currentDisplay: '',
			total: 0.0,
			currentOperation: 'add'
		}
	},

	methods: {
		clear(){
			this.currentDisplay = '';
			this.current = '';
			this.total = 0.0;
		},

		append(num){
			this.currentDisplay += num;
			this.current += num;
		},

		operate(op){
			
			if(op != 'dot'){
				this.currentOperation = op;
			}
			
			let num;

			switch(op){
				case 'add':
					this.currentDisplay += '+';
					if(this.current === '') return;
					num = parseFloat(this.current);
					this.total = this.total === 0? num : this.total+num;
					this.current = '';

				break
				case 'subtract':
					this.currentDisplay += '-';
					if(this.current === ''){ 
						this.current += '-'
						return;
					}
					num = parseFloat(this.current);
					this.total = this.total === 0? num : this.total-num;
					this.current = '';
				break
				case 'multiply':
					this.currentDisplay += 'x';
					if(this.current === '') return;
					num = parseFloat(this.current);
					this.total = this.total === 0? num : this.total*num;
					this.current = '';
				break
				case 'divide':
					this.currentDisplay += '/';
					if(this.current === '') return;
					num = parseFloat(this.current);
					this.total = this.total === 0? num : this.total/num;
					this.current = '';
				break
				case 'percent':
					this.currentDisplay += '%';
					if(this.current === '') return;
					num = parseFloat(this.current);
					this.total = this.total === 0? num/100 : this.total/100;
					this.current = '';
				break
				case 'dot':
					if(this.current.indexOf('.') != -1) return;
					this.currentDisplay += '.';
					if(this.current === ''){ 
						this.current += this.total;
						this.total = 0;
					}
					this.current += '.';
					
					console.log(this.current)
				break
				case 'invert':
					if(this.currentDisplay.charAt(0) === '-'){
						this.currentDisplay = this.currentDisplay.replace(/-/, '');
					}
					else{
						this.currentDisplay = '-' + this.currentDisplay;
					}
					if(this.current === '') return;
					this.current *= -1;
				break
				default:
					return;
			}
		},

		calculate(){
			this.operate(this.currentOperation);
			this.currentDisplay = this.total.toString();
		}
	}
}

</script>


<style scoped>
	.calculator {
		font-size: 40px;
		max-width: 800px;
		margin: auto;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-columns: (50px, 100px);
		grid-auto-rows: minmax(50px, auto);
		border: 1px solid #999;
	}

	.display{
		grid-column: 1 / 5;
		background-color: #222;
		color: #eee;
		text-align: right;
		line-height: 80px;
		padding-right: 20px;
		padding-left: 20px;
		min-height: 80px;
		overflow-x: auto;
	}

	.zero{
		grid-column: 1 / 3;
	}

	.calculator_key{
		background-color: #F2F2F2;
		border: 1px solid #999;
		user-select: none;
	}
	.calculator_key:active{
		background-color: lightblue;
	}

	/* To make hover work in touchscreen devices */
	@media(hover: hover) and (pointer: fine) {
		.calculator_key:hover{
			background-color: lightblue;
			cursor: pointer;
		}
	}
</style>
