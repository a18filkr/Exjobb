<template>
  <li>{{ name }}</li>
</template>

<script>
export default {
  props: ['name'],
}
</script>

<style scoped>
  li {
    text-decoration: none;
    list-style: none;
    background: #2c3e50;
    color: #e65a33;
    padding: 20px;
    max-width: 400px;
    margin: 5px auto;
    border-radius: 5px;
  }
</style>