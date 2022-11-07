<template>
  <div class="modal-backdrop">
    <div class="modal">
      <slot name="header">
        <v-card-title>Add Stock</v-card-title> 
        <button type="button" class="btn-close" @click="close"> x </button>
      </slot>
      <slot name="body">

          <div class="initial-data-sort">
    <input type="search" v-model="search" placeholder="Search" />
    
        <v-card elevation="2" tile v-for="portfolio in filteredlist" :key="portfolio.id">
        <v-row no-gutters>
          <v-col cols="12" sm="10">
            <v-card-title>{{ portfolio.symbol }} </v-card-title>
            <v-card-text>Last Price: {{ portfolio.lastPrice }} - weightedAvgPrice: {{ portfolio.weightedAvgPrice }}</v-card-text>
          </v-col>
          <v-col cols="12" sm="2">
          <v-card-text>
          <v-btn  @click="addportfolio(portfolio.symbol,portfolio.lastPrice,portfolio.weightedAvgPrice)" depressed color="success">Add </v-btn></v-card-text>
          </v-col>
          </v-row>
        </v-card>
  </div>
      </slot>
    </div>
  </div>
</template>
<style>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9
  }
  input {
    border-radius: 4px;
    border: 1px solid #dbdbdb;
    height: 36px;
    width: 100%;
    padding: 0 20px;
    margin: 0 0;
}
.modal {
    padding: 20px;
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 760px;
    height: 420px;
    position: relative
}

  .initial-data-sort{
    overflow:auto
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    padding: 10px;
    cursor: pointer;
    background: #105591;
    color: white;
}
</style>
<script>

  import axios from 'axios'

  export default {
    name: 'Modal',
    data() {
      return {
        coins: [],
        portfolios: [],
        search: null
      }
    },
    props: {
      onselectionchange: Function,
    },
    methods: {
      addportfolio(symbol,lastPrice,weightedAvgPrice) {
        this.portfolios.push({ symbol: symbol, lastPrice: lastPrice, weightedAvgPrice: weightedAvgPrice, count:1 });
        this.onselectionchange(this.portfolios);
      },
      getcoins() {
        axios.get('https://api2.binance.com/api/v3/ticker/24hr')
          .then(response => {
            this.coins = response.data;
          })
          .catch(error => console.log(error));
      },
      close() {
        this.$emit('close');
      }
    },
    computed: {
      filteredlist: function() {
        let searchTerm = (this.search || "").toLowerCase()
        return this.coins.filter(function(item) {
          let symbol = (item.symbol || "").toLowerCase()
          return symbol.indexOf(searchTerm) > -1
        })
      }
    },
    created() {
      this.getcoins();
      setInterval(function () {
        this.getcoins();
      }.bind(this), 20000); 
    }
  };
</script>