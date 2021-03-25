<template>
  <Button class="clicker" text="Klicka!" v-if="showClicker" @tap="stopTimer">
  </Button>
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
    font-weight: bold;
    text-align: center;
    font-size: 24;
    padding: 55 0;
    margin: 30px auto;
  }
</style>