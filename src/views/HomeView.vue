<template>
  <div class="harga">
    <h1>Harga Bitcoin Terhadap Mata Uang Asing</h1>
    <table>
      <thead>
        <tr>
          <th>Mata Uang</th>
          <th>Harga Beli</th>
          <th>Harga Jual</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(rate, currency) in rates" :key="currency">
          <td>{{ currency }}</td>
          <td>{{ rate.buy }}</td>
          <td>{{ rate.sell }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "HomeView",
  data() {
    return {
      rates: {},
    };
  },
  created() {
    axios
      .get('https://blockchain.info/ticker')
      .then((response) => {
        this.rates = {
        AUD: response.data.AUD,
        EUR: response.data.EUR,
        GBP: response.data.GBP,
        JPY: response.data.JPY,
        USD: response.data.USD,
      };
      })
      .catch((error) => {
        console.log(error);
      });
  },
 
};
</script>

