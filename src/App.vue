<template>
  <div id="app">
    <header>
      <h1>Currency converter</h1>
    </header>
    <main>
		<div v-for="(value, key) in currenciesList" :key="key">
			<currencyInput 
				class="currencyInput" 
				:name="currenciesList[key].name" 
				:country="currenciesList[key].country" 
				:countryFlag="currenciesList[key].countryFlag"
				:value="inputValue"
			/>
		</div>
	</main>
  </div>
</template>

<script>
/* eslint-disable */
import currencies from "@/assets/data/currencies.json";
import currencyInput from "@/components/currencyInput.vue"

export default {
	name: "App",
	data() {
		return {
			currenciesList: currencies.currencies,
			inputValue: 12,
		};
	},
	methods: {},
	components: {
		currencyInput
	},
	watch: {},
	created() {},
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
