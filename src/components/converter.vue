<template>
   
    <div class="container">
      <div class="currency">
         <select @change="compute()" v-model="selected"  id="input_currency">
         <option v-for="option in options" :key="option" :value="option.value">
            {{ option.text }}
         </option>
         </select>
          <!--<input @input="compute()" type="number" name="" id="input_amount" v-model="input_amount">-->
          <v-text-field  @input="compute()" label="Введите сумму" variant="outlined" clearable  v-model="input_amount"></v-text-field>
      
      </div>

      <v-btn id="exchange" icon="mdi-open-in-new" variant="tonal" v-on:click="changeValuta()">
         ↕
      </v-btn>

      <div class="currency">
         <select @change="compute()" v-model="selected2" id="output_currency">
         <option v-for="option in options" :key="option" :value="option.value">
            {{ option.text }}
         </option>
         </select>
         <v-text-field  @input="compute()" label="Введите сумму" variant="outlined" clearable  v-model="output_amount"></v-text-field>
      
      </div>
      <div class="result">
              <div class="rate" id="rate">{{ rate }}</div>
      </div>
  </div>

</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      info: null,
      rate: '',
      selected: 'KZT',
      input_amount: '1',
      selected2: 'RUB',
      output_amount: '0',
      options: [
         { text: 'AED', value: 'AED' },
         { text: 'ARS', value: 'ARS' },
         { text: 'AUD', value: 'AUD' },
         { text: 'BGN', value: 'BGN' },
         { text: 'BRL', value: 'BRL' },
         { text: 'BSD', value: 'BSD' },
         { text: 'CAD', value: 'CAD' },
         { text: 'CHF', value: 'CHF' },
         { text: 'CLP', value: 'CLP' },
         { text: 'CNY', value: 'CNY' },
         { text: 'COP', value: 'COP' },
         { text: 'CZK', value: 'CZK' },
         { text: 'DKK', value: 'DKK' },
         { text: 'DOP', value: 'DOP' },
         { text: 'EGP', value: 'EGP' },
         { text: 'EUR', value: 'EUR' },
         { text: 'FJD', value: 'FJD' },
         { text: 'GBP', value: 'GBP' },
         { text: 'GTQ', value: 'GTQ' },
         { text: 'HKD', value: 'HKD' },
         { text: 'HRK', value: 'HRK' },
         { text: 'HUF', value: 'HUF' },
         { text: 'IDR', value: 'IDR' },
         { text: 'ILS', value: 'ILS' },
         { text: 'INR', value: 'INR' },
         { text: 'ISK', value: 'ISK' },
         { text: 'JPY', value: 'JPY' },
         { text: 'KRW', value: 'KRW' },
         { text: 'KZT', value: 'KZT' },
         { text: 'MXN', value: 'MXN' },
         { text: 'MYR', value: 'MYR' },
         { text: 'NOK', value: 'NOK' },
         { text: 'NZD', value: 'NZD' },
         { text: 'PAB', value: 'PAB' },
         { text: 'PEN', value: 'PEN' },
         { text: 'PHP', value: 'PHP' },
         { text: 'PKR', value: 'PKR' },
         { text: 'PLN', value: 'PLN' },
         { text: 'PYG', value: 'PYG' },
         { text: 'RON', value: 'RON' },
         { text: 'RUB', value: 'RUB' },
         { text: 'SAR', value: 'SAR' },
         { text: 'SEK', value: 'SEK' },
         { text: 'SGD', value: 'SGD' },
         { text: 'THB', value: 'THB' },
         { text: 'TRY', value: 'TRY' },
         { text: 'TWD', value: 'TWD' },
         { text: 'UAH', value: 'UAH' },
         { text: 'USD', value: 'USD' },
         { text: 'UYU', value: 'UYU' },
         { text: 'VND', value: 'VND' },
         { text: 'ZAR', value: 'ZAR' }
      ],

   }
  },
  methods:{
    changeValuta(){
         const temp = this.selected;
         this.selected = this.selected2;
         this.selected2= temp;
         this.compute()
         
      },
      async compute(){
         const input_currency1 = this.selected;
         const output_currency1 = this.selected2;
         console.log(input_currency1,output_currency1)
         let result = await axios.get(`https://api.exchangerate-api.com/v4/latest/${input_currency1}`);
         const new_rate = result.data.rates[output_currency1];
         this.rate = `1 ${input_currency1} = ${new_rate} ${output_currency1}`
         this.output_amount = (this.input_amount * new_rate).toFixed(2);
      }
  },
  mounted() {
     this.compute();
  }
  
  }
</script>

<style>
body{
   background-color: rgb(240, 225, 205);
   display: flex;
   justify-content: center;
   text-align: center;
   font-family: Verdana, Geneva, Tahoma, sans-serif;
   font-size: 25px;
}
 
.container{
   /*height: 500px;
   width: 500px;*/
   /* background-image: linear-gradient(to bottom left,#a4d1a2,#b1eece ); */
   background-color:#ffffff;
   margin-top: 10vh;
   padding:20px;
   border: none;
   border-radius: 20px;
   box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
   color: #000000;
   opacity: 1;
   text-align: center;
   align-content: center;
}

.currency{
   display: flex;
   align-items: center;
   padding-top: 5%;
   padding-bottom: 5%;
   
}
.v-input__details{
   display: none !important;
}

.currency select {
   font-family: Verdana, Geneva, Tahoma, sans-serif;
background-color:transparent;
color: #0e3114;
width : 80px;
height: 32px;
border: none;
border-radius: 5px;
font-size: 1.5rem;
font-weight: bold;

}

.currency input {
   font-family: Verdana, Geneva, Tahoma, sans-serif;

   background-color: transparent;
   color: #192c1e;
   width: 400px;
   height: 40px;
   border: none;
   border-radius: 30px;
   padding:2px;
   font-size: 1.8rem;
   font-weight: 500;
   margin-top: 4px;
   
}
.currency select option{
   background-color: #89c095;
   font-size: 1rem;
   color: rgb(20, 41, 26);
   
}

.result {

   display: flex;
  align-items: center;
  justify-content: center;
}

button#exchange  {
   width: 80px;
   height: 80px;
   margin-top: 15px;
   margin-bottom: 15px;
   background-color: transparent;
   color:#213a25;
   font-weight: bold;
   font-size: 2.5rem;
   text-align: center;
   justify-content: center;
   padding-bottom : 0.3rem;
   border: none;
  /* border: 2px solid #000;*/
   border-radius: 50%;
}

button#exchange:hover{
   color: #213a25;
   background-color: #569456;
   border: none;
   border-radius: 50%;
}

button#exchange:active{
}

.rate{
  
   color: #5f2419;    
   width: 500px;
   height: 35px;
   border-radius: 15px   ;
   border-radius: 35px;
   margin-top: 80px;
   font-weight: 500;
   font-size: 2rem;
   text-align: center;
}

select:focus, input:focus, button:focus {
  outline: 0;
}
</style>