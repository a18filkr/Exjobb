<template>
    <Label class="country" textWrap="true">{{ name }}</Label>
</template>

<script>
export default {
  props: ['name'],
}
</script>

<style scoped>
  .country {
    background: #2c3e50;
    color: #e65a33;
    padding: 35px;
    max-width: 400px;
    margin: 5px auto;
    border-radius: 5px;
    text-align: center;

  }
</style>