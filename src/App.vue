<template>
  <div id="app">
    <header>
      <h1>Currency converter</h1>
    </header>
    <main>
		<currencyInput :name="currencies.name" :country="currencies.country" :countryFlag="currencies.countryFlag" />
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
			currencies: currencies.currencies[0],
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
</style>
