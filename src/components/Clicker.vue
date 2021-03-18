<template>
  <div class="clicker" v-if="showClicker" @click="stopTimer">
    KLICKA!
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showClicker: false,
      timer: null,
      reactionTime: 0
    }
  },
  // Hook när component läggs in
  mounted() {
    console.log('mounted')
    setTimeout(() => {
      this.showClicker = true
      this.startTimer()
      console.log(this.delay)
    }, this.delay)
  },
  // Hook när något i component uppdateras
  updated() {
    console.log('updated')
  },
  // Hook när component tas bort
  unmounted() {
    console.log('unmounted')
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10
      }, 10)
    },
    stopTimer() {
      clearInterval(this.timer)
      console.log(this.reactionTime)
      this.$emit('reactionTime', this.reactionTime)
    }
  }
}
</script>

<style>
  .clicker {
    width: 70%;
    border-radius: 15px;
    background: #2c3e50;
    color: #e65a33;
    font-size: 1.5rem;
    font-weight: bold;
    text-align: center;
    padding: 120px 0;
    margin: 30px auto;
  }
</style>