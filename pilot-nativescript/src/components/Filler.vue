<template>
  <Label class="joke" textWrap="true">{{ joke }}</Label>
</template>

<script>
export default {
  props: ['joke'],
}
</script>

<style scoped>
  .joke {
    background: #2c3e50;
    color: #e65a33;
    padding: 20px;
    max-width: 400px;
    margin: 5px auto;
    border-radius: 5px;
  }
</style>