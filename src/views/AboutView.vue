<template>
  <div>
    <h1>Konversi Rupiah ke Bitcoin</h1>
    <div>
      <label>Masukkan nilai Rupiah:</label>
      <input type="text" v-model="rupiah" />
      <button @click="convertToBitcoin()">Konversi ke Bitcoin</button>
    </div>
    <div v-if="bitcoin">
      <p>{{ rupiah }} Rupiah setara dengan {{ bitcoin }} Bitcoin.</p>
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
      rupiah: '',
      bitcoin: '',
      error: '',
    };
  },
  methods: {
    async convertToBitcoin() {
      try {
        const response = await fetch(`https://blockchain.info/tobtc?currency=USD&value=${this.rupiah / 14000}`);
        const data = await response.text();
        this.bitcoin = data;
        this.error = '';
      } catch (error) {
        this.error = 'Terjadi kesalahan saat mengambil data.';
        this.bitcoin = '';
      }
    },
  },
};
</script>
