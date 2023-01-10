<template>
<!-- eslint-disable -->
	<div id="app">
		<header>
		<h1>Currency converter</h1>
		</header>
		<main>
			<!------------------------------>
            <button class="btn">Button</button>
		</main>
  	</div>
</template>

<script>
/* eslint-disable */
import DaisyUI from 'daisyui'

export default {
	name: "App",
	data() {
		return {
            apiLink: "https://v6.exchangerate-api.com/v6/" + this.apiKey + "/latest/" + this.baseCurrency,
            apiKey: "d57569bf593ebb534d9227a5",
            baseCurrency: "USD",
		};
	},
	methods: {

	},
	created() {

	},
};
</script>

<style src="./app.css" />

<!--<style scoped>-->
<!--#app {-->
<!--	font-family: Avenir, Helvetica, Arial, sans-serif;-->
<!--	-webkit-font-smoothing: antialiased;-->
<!--	-moz-osx-font-smoothing: grayscale;-->
<!--	text-align: center;-->
<!--	color: #2c3e50;-->
<!--	padding: 0;-->
<!--	margin: 0;-->
<!--	height: 100vh;-->
<!--}-->
<!--header {-->
<!--	display: flex;-->
<!--	justify-content: center;-->
<!--	align-items: center;-->
<!--	padding: 20px;-->
<!--	background-color: #212121;-->
<!--	color: #fff;-->
<!--}-->
<!--main {-->
<!--	display: flex;-->
<!--	flex-direction: column;-->
<!--	align-items: center;-->
<!--	justify-content: center;-->
<!--	margin-top: 20px;-->
<!--}-->
<!--.converter {-->
<!--	margin: 8px;-->
<!--    padding: 8px;-->
<!--	background-color: #212121;-->
<!--    color: white;-->
<!--    border-radius: 9px;-->
<!--	min-width: 580px;-->
<!--	max-width: 580px;-->
<!--}-->
<!--.input {-->
<!--    display: flex;-->
<!--    flex-direction: row;-->
<!--    justify-content: space-between;-->
<!--}-->
<!--.left-box {-->
<!--    display: flex;-->
<!--    flex-direction: column;-->
<!--    margin-left: 16px;-->
<!--	cursor: pointer;-->
<!--}-->
<!--.currency-name {-->
<!--    color: white;-->
<!--    font-size: 32px;-->
<!--    font-weight: 500;-->
<!--    text-align: start;-->
<!--    justify-content: flex-start;-->
<!--    margin-left: 0;-->
<!--}-->
<!--.currency-country {-->
<!--    color: #5fcf80;-->
<!--    font-size: 24px;-->
<!--    font-weight: 300;-->
<!--    text-align: start;-->
<!--    justify-content: flex-start;-->
<!--    margin-left: 0;-->
<!--}-->
<!--.right-box {-->
<!--    display: flex;-->
<!--    flex-direction: row;-->
<!--    margin-left: 16px;-->
<!--    margin-right: 16px;-->
<!--    width: 50%;-->
<!--}-->
<!--.right-box input {-->
<!--    margin-right: 0;-->
<!--    margin-left: auto;-->
<!--    text-align: end;-->
<!--    font-size: 32px;-->
<!--    color: white;-->
<!--    outline: none;-->
<!--    border: none;-->
<!--    background: transparent;-->
<!--    height: 100%;-->
<!--    width: 100%;-->
<!--}-->
<!--.drop-down {-->
<!--	max-height: 305px;-->
<!--	overflow-y: auto;-->
<!--	margin-top: 12px;-->
<!--}-->
<!--.btn {-->
<!--	padding: 19px 39px 18px 39px;-->
<!--	color: #FFF;-->
<!--	background-color: #4bc970;-->
<!--	font-size: 18px;-->
<!--	text-align: center;-->
<!--	font-style: normal;-->
<!--	border-radius: 5px;-->
<!--	width: 100%;-->
<!--	border: 1px solid #3ac162;-->
<!--	border-width: 1px 1px 3px;-->
<!--	box-shadow: 0 -1px 0 rgba(255, 255, 255, 0.1) inset;-->
<!--	margin: 20px;-->
<!--	cursor: pointer;-->
<!--	max-width: 350px;-->
<!--	min-width: 350px;-->
<!--}-->
<!--.drop-down::-webkit-scrollbar {-->
<!--  width: 8px;-->
<!--}-->

<!--.drop-down::-webkit-scrollbar-track {-->
<!--  background: #191919;-->
<!--  border-radius: 8px;-->
<!--}-->

<!--.drop-down::-webkit-scrollbar-thumb {-->
<!--  background: #5fcf80;-->
<!--  border-radius: 4px;-->
<!--}-->
<!--.element {-->
<!--	background-color: #212121;-->
<!--	cursor: pointer;-->
<!--	padding: 12px;-->
<!--}-->
<!--.element:hover {-->
<!--  background: radial-gradient(circle, rgba(59,59,59,1) 0%, rgba(33,33,33,1) 100%);-->
<!--}-->
<!--.btn-remove {-->
<!--  display: flex;-->
<!--  align-items: center;-->
<!--  justify-content: center;-->
<!--  margin-left: 15px;-->
<!--}-->
<!--</style>-->
