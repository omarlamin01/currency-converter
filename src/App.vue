<template>
<!-- eslint-disable -->
	<div id="app">
		<header>
		<h1>Currency converter</h1>
		</header>
		<main>
			<!------------------------------>
			<div class="converter">
				<div class="input">
					<div class="left-box">
						<span class="currency-name">{{ activeCurrenciy1.name }}</span>
						<span class="currency-country">{{ activeCurrenciy1.country }}</span>
					</div>
					<div class="right-box">
						<input
							type="number"
							min="0"
							v-model="currencyInput1"
							@change="converterA"
						>
					</div>
				</div>
				<div class="drop-down">
					<div
						class="element"
						v-for="currency in currenciesList"
					>
						<span class="currency-name">{{ currency.name }}</span>
						<span class="currency-country"> - ({{ currency.country }})</span>
					</div>
				</div>
			</div>
			<!------------------------------>
			<div class="converter">
				<div class="input">
					<div class="left-box">
						<span id="currency-name">{{ activeCurrenciy2.name }}</span>
						<span id="currency-country">{{ activeCurrenciy2.country }}</span>
					</div>
					<div class="right-box">
						<input 
							type="number"
							min="0"
							maxlength="4"
							v-model="currencyInput2"
							@change="converterB"
						>
					</div>
				</div>
				<div class="drop-down">
					<div
						class="element"
						v-for="currency in currenciesList"
					>
						<span class="currency-name">{{ currency.name }}</span>
						<span class="currency-country"> - ({{ currency.country }})</span>
					</div>
				</div>
			</div>
			
		</main>
  	</div>
</template>

<script>
/* eslint-disable */
import data from "@/assets/data/currencies.json";
import currencyInput from "@/components/currencyInput.vue"

export default {
	name: "App",
	data() {
		return {
			currenciesList: data.currencies,
			activeCurrenciy1: data.currencies[0],
			activeCurrenciy2: data.currencies[1],
			currencyInput1:  10,
			currencyInput2:  1,
		};
	},
	methods: {
		formatNumber(number, digits) {
			let floor = parseInt(number);
			let float = parseInt((number - floor) * Math.pow(10, digits))
			if (float < Math.pow(10, (digits - 1))) {
				return (floor + '.' + float + '0');
			} else {
				return (floor + '.' + float);
			}
		},
		converterA() {
			this.currencyInput1 = this.formatNumber(this.currencyInput1, 2);
			this.currencyInput2 = this.formatNumber((this.activeCurrenciy2.valueToUSD * (this.currencyInput1 / this.activeCurrenciy1.valueToUSD)), 2);
		},
		converterB() {
			this.currencyInput2 = this.formatNumber(this.currencyInput2, 2);
			this.currencyInput1 = this.formatNumber((this.activeCurrenciy1.valueToUSD * (this.currencyInput2 / this.activeCurrenciy2.valueToUSD)), 2);
		}
	},
	components: {
		currencyInput
	},
	watch: {
		converterA(currencyInput1) {
			this.currencyInput2 = activeCurrenciy2.valueToUSD * (this.currencyInput1 / activeCurrenciy1.valueToUSD);
			console.log(this.currencyInput2);
		},
		converterB(currencyInput2) {
			this.currencyInput1 = activeCurrenciy1.valueToUSD * (this.currencyInput2 / activeCurrenciy2.valueToUSD);
		}
	},
	created() {
		this.currencyInput1 = this.formatNumber(this.currencyInput1, 2);
		this.currencyInput2 = this.formatNumber(this.currencyInput2, 2);
	},
	};
</script>

<style scoped>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	padding: 0;
	margin: 0;
}
header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 20px;
	background-color: #212121;
	color: #fff;
}
main {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}
.input {
    margin: 8px;
    padding: 8px;
    display: flex;
    flex-direction: row;
    background-color: #212121;
    color: white;
    border-radius: 9px;
    justify-content: space-between;
	min-width: 580px;
	max-width: 580px;
}
.left-box {
    display: flex;
    flex-direction: column;
    margin-left: 16px;
	cursor: pointer;
}
.currency-name {
    color: white;
    font-size: 32px;
    font-weight: 500;
    text-align: start;
    justify-content: flex-start;
    margin-left: 0;
}
.currency-country {
    color: rgba(255, 255, 255, 0.7);
    font-size: 24px;
    font-weight: 300;
    text-align: start;
    justify-content: flex-start;
    margin-left: 0;
}
.right-box {
    display: flex;
    flex-direction: column;
    margin-left: 16px;
    margin-right: 16px;
    width: 50%;
}
.right-box input[type="number"] {
    margin-right: 0;
    margin-left: auto;
    text-align: end;
    font-size: 32px;
    color: white;
    outline: none;
    border: none;
    background: transparent;
    height: 100%;
    width: 50%;
}
.element {
	background-color: #212121;
}
</style>
