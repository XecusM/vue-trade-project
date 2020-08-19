<template lang="html">
  <div class="row">
    <appStock v-for="stock in stocks" :stock="stock"></appStock>
  </div>
</template>

<script>
  import Stock from './Stock.vue'
  export default {
    components: {
      appStock: Stock
    },
    computed: {
      stocks(){
        return this.$store.getters.stocks
      }
    }
  }
</script>

<style lang="css" scoped>
</style>
