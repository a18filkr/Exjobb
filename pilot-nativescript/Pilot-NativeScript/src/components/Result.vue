<template>
    <StackLayout>
    <Label class="message" height="auto">Din reaktionstid: {{ time }}</Label>
    <Label class="rank"> {{rank}} </Label>
    </StackLayout>
</template>

<script>
export default {
  props: ['time'],
  data() {
    return {
      rank: null,
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
    font-size: 20;
    font-weight: bold;
    color: #e65a33;
    text-align: center;
    padding: 20 0;
  }

  .message {
      vertical-align: center;
      text-align: center;
      font-size: 20;
      color: #333333;
      padding: 20 0;
  }
</style>