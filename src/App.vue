<template>
  <div id="app">
    <header>
      <h1>Currency converter</h1>
    </header>
    <main>
		<div v-for="(value, key) in activeCurrencies" :key="key">
			<currencyInput 
				class="currencyInput" 
				:name="activeCurrencies[key].name" 
				:country="activeCurrencies[key].country" 
				:countryFlag="activeCurrencies[key].countryFlag"
			/>
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
			activeCurrencies: data.activeCurrencies,
			inputValue:  0,
		};
	},
	methods: {},
	components: {
		currencyInput
	},
	watch: {},
	created() {
		if (this.activeCurrencies.length < 2) {
			this.activeCurrencies = [];
			this.activeCurrencies.push(this.currenciesList[0]);
			this.activeCurrencies.push(this.currenciesList[1]);
		}
		
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
.currencyInput {
	min-width: 580px;
	max-width: 580px;
}
</style>
