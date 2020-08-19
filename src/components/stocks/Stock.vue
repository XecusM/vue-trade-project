<template lang="html">
  <div class="col-sm-6 col-md-4">
    <div class="card" style="max-width: 18rem;">
      <div class="card-header text-white bg-success mb-3">
        {{ stock.name }}
        <small>(price: {{ stock.price }})</small>
      </div>
      <div class="card-body row">
        <div class="col-8">
          <div class="float-left">
            <input
                  type="number"
                  class="form-control"
                  placeholder="Quantity"
                  v-model.number="quantity">
          </div>
        </div>
        <div class="col-4">
          <div class="float-right">
            <button
                    type="button"
                    class="btn btn-success"
                    @click="buyStock"
                    :disabled="quantity <= 0 || !Number.isInteger(quantity)">
              Buy
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

</style>
