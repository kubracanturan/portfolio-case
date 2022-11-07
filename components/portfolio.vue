<template>
  <div class="initial-data-sort">
        <div v-for="(portfolio, index) in portfolios" :key="portfolio.id">
         <v-row no-gutters>
          <v-col cols="12" sm="8">
            <v-card-title>{{ portfolio.symbol }} </v-card-title>
            <v-card-text>Last Price: {{ portfolio.lastPrice }} - weightedAvgPrice: {{ portfolio.weightedAvgPrice }}</v-card-text>
          </v-col>
          <v-col cols="12" sm="2">
            <v-card-text><input type="number" class="ma-2" name="count" id="count" v-model="portfolio.count" /></v-card-text>
          </v-col>
          <v-col cols="12" sm="2">
            <v-card-text><v-btn class="ma-2" outlined color="indigo" @click="removeitem(portfolio, index)">Remove</v-btn></v-card-text>
          </v-col>
          </v-row>
        </div>
  </div>
</template>

<script>
  import axios from 'axios'

  
  export default {
    name: 'portfoliolist',
    props: {
      portfolios: Array,
    },
    methods: {
      removeitem: function (portfolio, index) {
          if(this.portfolios[index] === portfolio) { 
              this.portfolios.splice(index, 1)
          } else {
              let found = this.portfolios.indexOf(item)
              this.portfolios.splice(found, 1)
          }
      }
    }
  }
</script>