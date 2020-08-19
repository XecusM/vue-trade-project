<template lang="html">
  <div class="col-md-6">
    <div class="card">
      <div class="card-header text-white bg-success mb-3">
        {{ stock.name }}
        <small>(price: {{ stock.price }})</small>
      </div>
      <div class="card-body row">
        <div class="col-6">
          <div class="float-left">
            <input
                  type="number"
                  class="form-control"
                  placeholder="Quantity"
                  v-model.number="quantity"
                  :class="{danger: insufficientFunds}">
          </div>
        </div>
        <div class="col-6">
          <div class="float-right">
            <button
                    type="button"
                    class="btn btn-success"
                    @click="buyStock"
                    :disabled="insufficientFunds || quantity <= 0 || !Number.isInteger(quantity)">
              {{ insufficientFunds ? 'Insufficient Funds' : 'Buy' }}
            </button>
          </div>
        </div>
      </div>
    </div>
    <br>
  </div>
</template>

<script>
export default {
  props: ['stock'],
  data(){
    return {
      quantity: 0
    }
  },
  computed: {
    funds(){
      return this.$store.getters.funds
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds
    }
  },
  methods:{
    buyStock(){
      const order = {
        stockId: this.stock.id,
        quantity: this.quantity,
        stockPrice: this.stock.price
      }
      this.$store.dispatch('buyStock', order)
      this.quantity = 0
    },
  }
}
</script>

<style lang="css" scoped>
  .danger{
    border: 1px solid red;
  }
</style>
