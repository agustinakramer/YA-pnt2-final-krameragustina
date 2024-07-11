<template>
    <div class="currency-converter">
      <h1>Calculadora de Conversión de Moneda</h1>
      <div class="input-group">
        <label for="pesos">Ingresa la cantidad en pesos:</label>
        <input v-model.number="pesos" type="number" id="pesos" placeholder="Cantidad en pesos">
      </div>
      <div class="input-group">
        <label for="cotizacion">Cotización del Dólar (manual):</label>
        <input v-model.number="cotizacion" type="number" id="cotizacion">
      </div>
      <div class="input-group">
        <label for="resultado">Resultado en Dólares:</label>
        <input :value="resultado" type="number" id="resultado" disabled>
      </div>
      <div class="input-group">
        <label for="autoUpdate">Actualizar cotización automáticamente:</label>
        <input type="checkbox" id="autoUpdate" v-model="autoUpdate">
      </div>
      <p class="last-updated">Última actualización: {{ lastUpdated }}</p>
    </div>
  </template>

  <script>
  import axios from 'axios';

  export default {
    data() {
      return {
        pesos: 0,
        cotizacion: 0,
        autoUpdate: false,
        lastUpdated: null,
        intervalId: null
      };
    },
    computed: {
      resultado() {
        return (this.pesos / this.cotizacion).toFixed(2);
      }
    },
    watch: {
      autoUpdate(newValue) {
        if (newValue) {
          this.startAutoUpdate();
        } else {
          this.stopAutoUpdate();
        }
      }
    },
    methods: {
      async fetchCotizacion() {
        try {
          const response = await axios.get('https://api.bluelytics.com.ar/v2/latest');
          this.cotizacion = response.data.blue.value_sell;
          this.lastUpdated = new Date().toLocaleString();
        } catch (error) {
          console.error('Error fetching cotizacion:', error);
        }
      },
      startAutoUpdate() {
        this.fetchCotizacion();
        this.intervalId = setInterval(this.fetchCotizacion, 2000);
      },
      stopAutoUpdate() {
        if (this.intervalId) {
          clearInterval(this.intervalId);
          this.intervalId = null;
        }
      }
    },
    mounted() {
      this.fetchCotizacion();
    }
  };
  </script>

  <style scoped>
  .currency-converter {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #f9f9f9;
  }

  .input-group {
    margin-bottom: 15px;
  }

  .label {
    display: block;
    font-weight: bold;
    margin-bottom: 5px;
  }

  input[type="number"], input[type="checkbox"] {
    width: 100%;
    padding: 8px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 3px;
  }

  input[type="number"]:disabled {
    background-color: #eee;
  }

  .last-updated {
    margin-top: 15px;
    font-size: 14px;
    color: #666;
  }
  </style>
