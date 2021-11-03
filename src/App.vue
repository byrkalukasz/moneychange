<template>
  <div id="app">
    <select name="value" id="currency">
      <option v-for="item in list" v-bind:key="item.code">{{item.code}} kurs : {{item.mid}}</option>
    </select>
    <br>
    <label for="PLN">Ile chcesz wymienić PLN : </label>
    <input type="text" id="PLN"><br>
    <button v-on:click="convert()">Przelicz</button>
   
  </div>
</template>

<script>
import axios from 'axios'

export default{
  data()
  {
    return {list:undefined}
  },
  methods:{
    convert: function()
    {
      const cr = document.querySelector('#currency')
      const mid = this.list[cr.selectedIndex].mid
      const foreign = this.list[cr.selectedIndex].code
      const val = document.querySelector('#PLN').value
      const done = val / mid;
        alert("Otrzymasz: " + done + " " + foreign);
    }
  },
  mounted()
  {
    const url="http://api.nbp.pl/api/exchangerates/tables/A/?format=json"

    axios.get(url).then((resp) => 
    {this.list = resp.data[0].rates;
        console.log(this.list[1])
    });

  }
}
</script>

<style>

</style>
