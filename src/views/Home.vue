<template>
  <div class="home">
    <div class="error" v-if="showError">Plzz select the start date and end date.</div>
    <div class="d-flex">    
      <label class="offer-label">Give the end date for offer : </label>
      <input type="text" class="enddate offer-fields" name="end-date" placeholder="mm-dd-yyyy" v-model="endDate" />      
    </div>
    <a href="#" class="btn calculate-btn" @click.prevent="calculateTime()">Calculate</a>
    <timmer :enddate="endDate" :calculate="random"></timmer>
  </div>
</template>

<script>
// @ is an alias to /src
import timmer from '@/components/timmer.vue'

export default {
  name: 'Home',
  data() {
    return {    
      endDate: '',
      showTimer: false,
      showError: false,
      random: 0
    }
  },
  components: {
    timmer
  },
  methods: {
    calculateTime() {      
      if(this.endDate) {
        this.showTimer = true;
        this.showError = false;
        this.random = Math.random()*10
      }else {
        this.showError = true;
        this.showTimer = false;
      }
    }
  }
}
</script>
<style scoped>
.startdate {
  margin-right: 30px;
}
.offer-fields {
    height: 30px;
    min-width: 200px;
}
.error {
  color: red;
}
.calculate-btn {
  background: #0e0e0e;
    color: #fff;
    padding: 10px 30px;
    display: inline-block;
    margin: 40px 10px 10px 10px;
    text-decoration: none;
}
.offer-label {
  font-weight: bold;
}
</style>
