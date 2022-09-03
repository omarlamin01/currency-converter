<template>
<!-- eslint-disable -->
	<div id="app">
		<header>
		<h1>Currency converter</h1>
		</header>
		<main>
			<!------------------------------>
			<div class="converter" v-for="(active, key) in activeCurrencies" :key="key">
				<div class="input">
					<div class="left-box" @click="dropDowns[key] = !dropDowns[key]">
						<span class="currency-name">{{ active.name }}</span>
						<span class="currency-country">{{ active.country }}</span>
					</div>
					<div class="right-box">
						<input
							type="text"
							class="currencyInput"
							v-model="values[key]"
							@keyup="convertCurrencies(active, key)"
						>
						<div 
							class="btn-remove"
							@click="removeCurrency(active)"
							v-if="activeCurrencies.length > 2"
							style="cursor: pointer"
						>
							X
						</div>
					</div>
				</div>
				<div class="drop-down" v-show="dropDowns[key]">
					<div
						class="element"
						v-for="currency in filterCurrencies()"
						@click="setCurrency(key, currency)"
					>
						<span class="currency-name">{{ currency.name }}</span>
						<span class="currency-country"> ({{ currency.country }})</span>
					</div>
				</div>
			</div>
			<div class="add-button">
				<div class="btn" @click="showAddCurrencyDropDown = !showAddCurrencyDropDown">Add</div>
				<div class="drop-down" v-show="showAddCurrencyDropDown">
					<div
						class="element"
						v-for="currency in filterCurrencies()"
						@click="addCurrency(currency)"
					>
						<span class="currency-name">{{ currency.name }}</span>
						<span class="currency-country"> ({{ currency.country }})</span>
					</div>
				</div>
			</div>
		</main>
  	</div>
</template>

<script>
/* eslint-disable */
import data from "@/assets/data/currencies.json";

export default {
	name: "App",
	data() {
		return {
			currenciesList: data.currencies,
			activeCurrencies: [],
			values: [],
			dropDowns: [],
			showAddCurrencyDropDown: false,
		};
	},
	methods: {
		formatNumber(number, digits) {
			//separate integer part & float one
			let floor = parseInt(number);
			let float = (number - floor) * Math.pow(10, digits);

			//format float
			let major = parseInt((float - parseInt(float)) * 10);
			major >= 5 
				? float = parseInt(float) + 1 
				: float = parseInt(float)
			;
			float < Math.pow(10, (digits - 1))
				? float = '0' + float
				: float
			;

			//format integer part
			let str = floor.toString();
			if (str.length > 3) {
				floor = "";
				let triples = [];
				let nbTriples = Math.ceil(str.length / 3);
				for(var i = 0; i < nbTriples; i++) {
					triples.push(str.substring(str.length - (3 * i),str.length - (3 * i + 3)));
					if(i < nbTriples - 1)
						floor = ',' + triples[i] + floor;
					else
						floor = triples[i] + floor;
				}
			}
			return (floor + '.' + float);
		},
		deformatNumber(number) {
			if (number != '') {
				let isFormated = false;
				Array.from(number.toString()).forEach(digit => {
					if (digit == ',') {
						isFormated = true;
					}
				})
				if (isFormated) {
					let str = number.toString().split(',');
					number = "";
					str.forEach(part => {
						number += part;
					})
				}
				return parseFloat(number);
			} else 
				return number;
		},
		filterOnce(target) {
			let newArr = [];
			let index = 0;
			this.activeCurrencies.forEach(element => {
				if (element.id != target.id) {
					newArr.push({
						el: element,
						position: index
					});
				}
				index++;
			});
			return newArr;
		},
		filterCurrencies() {
			let newArr = [];
			this.currenciesList.forEach(element => {
				let isContained = false;
				this.activeCurrencies.forEach(target => {
					if (element.id == target.id)
						isContained = true;
				});
				if (!isContained) {
					newArr.push(element);
				}
			})
			return newArr;
		},
		addCurrency(currency) {
			if (this.activeCurrencies.length > 0) {
				this.activeCurrencies.push(currency);
				this.values.push(this.formatNumber(this.convertOnce(0, this.activeCurrencies.length - 1), 2));
				this.dropDowns.push(false);
			} else {
				this.activeCurrencies.push(currency);
				this.values.push(1.00);
				this.dropDowns.push(false);
			}
			this.showAddCurrencyDropDown = false;
		},
		removeCurrency(currency) {
			let newArr = [];
			this.activeCurrencies.forEach(element => {
				if (element.id != currency.id) {
					newArr.push(element);
				}
			});
			this.activeCurrencies = newArr;
		},
		convertOnce(from, to) {
			this.values[to] = this.formatNumber(((this.deformatNumber(this.values[from]) / this.activeCurrencies[from].valueToUSD) * this.activeCurrencies[to].valueToUSD), 2);
			this.values[from] = this.formatNumber(this.deformatNumber(this.values[from]), 2);
		},
		convertCurrencies(from, position) {
			this.filterOnce(from).forEach(element => {
				this.convertOnce(position, element.position);
			})
		},
		setCurrency(position, newCurrency) {
			this.activeCurrencies[position] = newCurrency;
			if (position == 0) {
				this.values[0] = 1.00;
				this.convertCurrencies(this.activeCurrencies[0], 0);
			} else {
				this.values[position] = this.convertOnce(0, position);
			}
			this.dropDowns[position] = false;
		}
	},
	created() {
		//set first two currencies
		this.addCurrency(this.currenciesList[0]);
		this.addCurrency(this.currenciesList[1]);
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
	height: 100vh;
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
	margin-top: 20px;
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
    color: #5fcf80;
    font-size: 24px;
    font-weight: 300;
    text-align: start;
    justify-content: flex-start;
    margin-left: 0;
}
.right-box {
    display: flex;
    flex-direction: row;
    margin-left: 16px;
    margin-right: 16px;
    width: 50%;
}
.right-box input {
    margin-right: 0;
    margin-left: auto;
    text-align: end;
    font-size: 32px;
    color: white;
    outline: none;
    border: none;
    background: transparent;
    height: 100%;
    width: 100%;
}
.drop-down {
	max-height: 305px;
	overflow-y: auto;
	margin-top: 12px;
}
.btn {
	padding: 19px 39px 18px 39px;
	color: #FFF;
	background-color: #4bc970;
	font-size: 18px;
	text-align: center;
	font-style: normal;
	border-radius: 5px;
	width: 100%;
	border: 1px solid #3ac162;
	border-width: 1px 1px 3px;
	box-shadow: 0 -1px 0 rgba(255, 255, 255, 0.1) inset;
	margin: 20px;
	cursor: pointer;
	max-width: 350px;
	min-width: 350px;
}
.drop-down::-webkit-scrollbar {
  width: 8px;
}

.drop-down::-webkit-scrollbar-track {
  background: #191919;
  border-radius: 8px;
}

.drop-down::-webkit-scrollbar-thumb {
  background: #5fcf80;
  border-radius: 4px;
}
.element {
	background-color: #212121;
	cursor: pointer;
	padding: 12px;
}
.element:hover {
	background-color: #121212;
}
</style>
