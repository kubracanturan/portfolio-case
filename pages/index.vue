<template>
  <v-row >
  <v-col cols="12">

  <banner />
  <div class="pa-4">  <v-btn
    depressed color="success"
        @click="showModal"
      >
        Add Stock
      </v-btn>
      <v-btn
      class="ma-2" outlined color="indigo"
        @click="onselectionchange()"
      >
        Update
      </v-btn></div>
    <Modal
      v-show="isModalVisible"
      @close="closeModal"
      :onselectionchange="onselectionchange"
    />
    </v-col>
    <v-col cols="12" sm="7" md="7">
     <portfoliolist :portfolios="portfolios" :onselectionchange="onselectionchange" />
    </v-col>
    <v-col cols="12" sm="5" md="5">
       <DoughnutChart :labels="labels" :counts="counts" />
    </v-col>
  </v-row>
</template>
<style>

.v-btn{
  position: initial
}
</style>
<script>
import DoughnutChart from '../components/doughnut'
import Modal from '../components/modal';
import portfoliolist from '../components/portfolio';
import banner from '../components/banner';

export default {
  name: 'App',
  components: { DoughnutChart, Modal, portfoliolist, banner },
  data: {
  },
  data() {
    return {
      isModalVisible: false,
      portfolios:[],
      labels:[],
      counts:[]
    };
  
  },
  methods: {
    onselectionchange(portfolios = this.portfolios) {
      this.portfolios = portfolios;
      const labels = [];
      const counts = [];
      for (let i = 0; i < this.portfolios.length; i++) {
        labels.push(this.portfolios[i].symbol);
        counts.push(this.portfolios[i].count);
      } 
      this.labels = labels;
      this.counts = counts;
      console.log(this.portfolios);
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  }
  
}
</script>