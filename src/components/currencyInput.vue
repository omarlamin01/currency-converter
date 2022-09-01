<template>
    <div class="input">
        <div class="left-box">
            <img :src="currency.countryFlag" :alt="'flag of ' + currency.country">
            <span id="currency-name">{{ currency.name }}</span>
        </div>
        <div class="right-box">
            <input type="number" v-model="model">
        </div>
    </div>
</template>

<script>
/* eslint-disable */
export default 
{
    name: "currencyInput",
    data() 
    {
        return 
        {
            model: 0
        };
    },
    props: {
        currency,
    },
};

</script>

<style scoped>

</style>