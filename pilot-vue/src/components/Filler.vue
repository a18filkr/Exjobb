<template>
  <p>{{ joke }}</p>
</template>

<script>
export default {
  props: ['joke'],
}
</script>

<style scoped>
  p {
    background: #2c3e50;
    color: #e65a33;
    padding: 20px;
    max-width: 400px;
    margin: 5px auto;
    border-radius: 5px;
  }
</style>