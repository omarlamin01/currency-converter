<template>
    <div class="input">
        <div class="left-box">
            <span id="currency-name">{{ name }}</span>
            <span id="currency-country">{{ country }}</span>
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
        name: String,
        country: String,
        countryFlag: String,
    },
};

</script>

<style scoped>

</style>