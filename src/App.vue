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
					<div class="left-box" @click="showDropDown1 = !showDropDown1">
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
				<div class="drop-down" v-show="showDropDown1">
					<div
						class="element"
						v-for="currency in filterCurrencies()"
					>
						<span class="currency-name">{{ currency.name }}</span>
						<span class="currency-country"> - ({{ currency.country }})</span>
					</div>
				</div>
			</div>
			<!------------------------------>
			<div class="converter">
				<div class="input">
					<div class="left-box" @click="showDropDown2 = !showDropDown2">
						<span class="currency-name">{{ activeCurrenciy2.name }}</span>
						<span class="currency-country">{{ activeCurrenciy2.country }}</span>
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
				<div class="drop-down" v-show="showDropDown2">
					<div
						class="element"
						v-for="currency in filterCurrencies(activeCurrenciy2.id)"
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
			showDropDown1: false,
			showDropDown2: false,
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
		filterCurrencies() {
			let newArr = [];
			this.currenciesList.forEach(element => {
				if (element.id != this.activeCurrenciy1.id && element.id != this.activeCurrenciy2.id)
					newArr.push(element);
			});
			return newArr;
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
.converter {
	margin: 8px;
    padding: 8px;
	background-color: #212121;
    color: white;
    border-radius: 9px;
	min-width: 580px;
	max-width: 580px;
}
.input {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
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
	cursor: pointer;
}
</style>
