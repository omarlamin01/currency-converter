<template>
  <div id="app">
    <header>
      <h1>Music player</h1>
    </header>
    <main>
		
	</main>
  </div>
</template>

<script>

import currencies from '@/assets/data/currencies.json';

export default {
	name: "App",
	data() {
		return {};
	},
	methods: {},
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
