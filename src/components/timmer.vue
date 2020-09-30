<template>
  <div class="timmer">
      <div class="d-flex timmer-wrapper" v-if="timmerDate">
        <div class="flex-1">
          <div class="number">{{timmerDate.days}}</div>
          <div class="label_number">DAYS</div>
        </div>
        <div class="flex-1">
          <div class="number">{{timmerDate.hours}}</div>
          <div class="label_number">HOURS</div>
        </div>
        <div class="flex-1">
          <div class="number">{{timmerDate.minutes}}</div>
          <div class="label_number">MINUTES</div>
        </div>

        <div class="flex-1">
          <div class="number seconds">{{timmerDate.seconds}}</div>
          <div class="label_number">SECONDS</div>
        </div>
      </div>
  </div>
</template>

<script>
export default {  
  data() {
    return {
      timmerDate: null
    }
  },
  props: {
    calculate: {
      default: false,
      required: false
    },
    enddate: {
      default: '',
      required: false
    }
  },
  mounted() {
    this.timmer();
  },
  watch: {
    calculate() {
      this.timmer();
    }
  },
  methods: {
    timmer() {   
      let endDate = new Date(this.enddate);
      endDate.setHours(23);
      endDate.setMinutes(59);
      endDate.setSeconds(59);   
      let startDate = (new Date()).getTime();
      let FinalEndDate = endDate.getTime();
      let time = FinalEndDate - startDate;

      let seconds = Math.floor((time / 1000) % 60);
      let minutes = Math.floor((time / 1000 / 60) % 60);
      let hours = Math.floor((time / (1000 * 60 * 60)) % 24);
      let days = Math.floor(time / (1000 * 60 * 60 * 24));

      if(time > 0) {
        this.timmerDate = {
          days: days < 10 ? '0'+days : days,
          hours: hours < 10 ? '0'+hours : hours,
          minutes: minutes < 10 ? '0'+minutes : minutes,
          seconds: seconds < 10 ? '0'+seconds : seconds
        }
        setTimeout(() => {
          this.timmer();
        }, 1000)
      }else {
        this.timmerDate = {
          days: '00',
          hours: '00',
          minutes: '00',
          seconds: '00'
        };
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flex-1 {
  flex-grow: 1;
}
.d-flex {
  display: flex;
}
.timmer-wrapper {
  max-width: 400px;
    margin: 20px auto;
    background: #000;
    color: #fff;
    padding: 10px;
    border-radius: 5px;
}
.number {
  font-size: 25px;
    padding-bottom: 10px;
}
.seconds {
  color: red;
}
</style>
