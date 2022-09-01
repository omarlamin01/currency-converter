<template>
    <div id="input">
        <div class="left-box">
            <span id="currency-name">{{ name }}</span>
            <span id="currency-country">{{ country }}</span>
        </div>
        <div class="right-box">
            <!-- eslint-disable-next-line -->
            <input type="number" v-model="value">
        </div>
    </div>
</template>

<script>
/* eslint-disable */
export default 
{
    name: "currencyInput",
    props: {
        name: String,
        country: String,
        countryFlag: String,
        value: Float64Array,
    },
};

</script>

<style scoped>
#input {
    margin: 8px;
    padding: 8px;
    display: flex;
    flex-direction: row;
    background-color: #212121;
    color: white;
    border-radius: 9px;
}
.left-box {
    display: flex;
    flex-direction: column;
    margin-left: 16px;
}
.left-box #currency-name {
    color: white;
    font-size: 32px;
    font-weight: 500;
    text-align: start;
    justify-content: flex-start;
    margin-left: 0;
}
.left-box #currency-country {
    color: rgba(255, 255, 255, 0.8);
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
    width: 100%;
}
</style>