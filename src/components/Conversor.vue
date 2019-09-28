<template>
    <div class="conversor">
        <h2>{{moedaA}} Para {{moedaB}} </h2>
        <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA"> 
        <input id="botaoconverter" type="button" value="Converter" v-on:click="converter">
        <h2>{{moedaB_value}}</h2>
    </div>
</template>

<script>
export default {
    name: "Conversor",
    props:["moedaA", "moedaB"],
    data(){
        return {
            moedaA_value: "",
            moedaB_value: 0,
        }
    },
    methods: {
        converter(){
            let de_para = this.moedaA + "_" + this.moedaB;
            let url = "https://free.currconv.com/api/v7/convert?q="+ 
            de_para+"&compact=ultra&apiKey=403a33c3bf8b2e1a1180";
            
            fetch(url)
            .then(res => {
                return res.json();
            })
            .then(json => {
                let cotacao = json[de_para];
                this.moedaB_value = (cotacao * parseFloat(this.moedaA_value)).toFixed(2);
            })
        }
    }
}
</script>
<style scoped>
    .conversor{
        max-width: 300px;
        padding: 20px;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    }
    .conversor input {
        border-radius: 2px;
        height: 30px;
    }
    #botaoconverter {
        margin-left: 2px;
        height: 35px;
        border: 1px solid blue;
        border-radius: 2px;
        background-color: rgb(95, 130, 243);
    }
</style>