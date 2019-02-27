<template>
  <p>{{ greeting }} World!</p>
</template>

<script>
  module.exports = {
    data: () => {
      return {
        greeting: 'Hello'
      }
    }
  }
</script>

<style lang="scss" scoped>
  $text-color: red;
  p {
    color: $text-color;
  }
</style>
