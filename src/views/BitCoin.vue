<template>
    <div>
      <h1>Konversi Bitcoin ke Rupiah</h1>
      <div>
        <label>Masukkan nilai Bitcoin:</label>
        <input type="text" v-model="bitcoin" />
        <button @click="convertToRupiah()">Konversi ke Rupiah</button>
      </div>
      <div v-if="rupiah">
        <p>{{ bitcoin }} Bitcoin setara dengan RP {{ rupiah }}</p>
      </div>
      <div v-if="error">
        <p>{{ error }}</p>
      </div>
    </div>
  </template>
  <script>
  export default {
    data() {
      return {
        bitcoin: '',
        rupiah: '',
        error: '',
      };
    },
    methods: {
      async convertToRupiah() {
        try {
          const response = await fetch(`https://blockchain.info/tobtc?currency=USD&value=${this.bitcoin}`);
          const bitcoinValue = await response.text();
          const rupiahValue = parseFloat(bitcoinValue) * 14000;
          this.rupiah = rupiahValue.toLocaleString('id-ID', {
            style: 'currency',
            currency: 'IDR',
          });
          this.error = '';
        } catch (error) {
          this.error = 'Terjadi kesalahan saat mengambil data.';
          this.rupiah = '';
        }
      },
    },
  };
  </script>