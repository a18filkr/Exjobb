<template>

    <p>Reaktionshastighet: {{ time }} ms</p>
    <p class="rank">{{rank}}</p>

</template>

<script>
export default {
  props: ['time'],
  data() {
    return {
      rank: null
    }
  },
  mounted() {
    if (this.time < 170 ) {
      this.rank = 'Chuck Norris!'
    } else if (this.time < 250) {
      this.rank = 'Snabb som djävulen!'
    } else if (this.time < 380) {
      this.rank = 'Snabbare kan du.'
    } else {
      this.rank = 'Min mormor kan bättre...'
    }
  }
}
</script>

<style scoped>
  .rank {
    margin: 10px 0;
    font-size: 1.4em;
    font-weight: bold;
    color: #e65a33;
  }
</style>