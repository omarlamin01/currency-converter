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
							:value="formatNumber(values[key], 2)"
							@change="convertCurrencies(active, key)"
						>
					</div>
					<div class="remove-btn" v-if="activeCurrencies.length > 2">
						<div class="btn" @click="removeCurrency(active)">remove</div>
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
				<div class="btn" @click="showAddCurrencyDropDown = !showAddCurrencyDropDown">+ add</div>
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
			let floor = parseInt(number);
			let float = parseInt((number - floor) * Math.pow(10, digits))
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
			
			if (float < Math.pow(10, (digits - 1))) {
				return (floor + '.' + float + '0');
			} else {
				return (floor + '.' + float);
			}
		},
		deformatNumber(number) {
			/*
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
					console.log(number);
				})
			}
			*/
			number = parseFloat(number);
			console.log(number);
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
			this.values[to] = (this.deformatNumber(this.values[from]) / this.activeCurrencies[from].valueToUSD) * this.activeCurrencies[to].valueToUSD;
		},
		convertCurrencies(from, position) {
			this.filterOnce(from).forEach(element => {
				this.convertOnce(position, element.position);
			})
		},
		setCurrency(position, newCurrency) {
			this.activeCurrencies[position] = newCurrency;
			this.values[position] = this.convertOnce(0, position);
			this.dropDowns[position] = false;
		}
	},
	created() {
		//set first two currencies
		this.addCurrency(this.currenciesList[Math.floor(Math.random() * this.currenciesList.length)]);
		this.addCurrency(this.currenciesList[Math.floor(Math.random() * this.currenciesList.length)]);
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
    flex-direction: column;
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
    width: 50%;
}
.drop-down {
	max-height: 305px;
	overflow-y: auto;
	margin-top: 12px;
}
.drop-down::-webkit-scrollbar {
  width: 8px;
}

.drop-down::-webkit-scrollbar-track {
  background: #1e1e1e;
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
</style>
