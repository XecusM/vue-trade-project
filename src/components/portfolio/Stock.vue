<template lang="html">
  <div class="col-md-6">
    <div class="card">
      <div class="card-header text-white bg-info mb-3">
        {{ stock.name }}
        <small>(price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
      </div>
      <div class="card-body row">
        <div class="col-6">
          <div class="float-left">
            <input
                  type="number"
                  class="form-control"
                  placeholder="Quantity"
                  v-model.number="quantity"
                  :class="{danger: insufficientQuantity}">
          </div>
        </div>
        <div class="col-6">
          <div class="float-right">
            <button
                    type="button"
                    class="btn btn-info"
                    @click="sellStock"
                    :disabled="insufficientQuantity || quantity <= 0 || !Number.isInteger(quantity)">
              {{ insufficientQuantity ? 'Not enough Stocks' : 'Sell' }}
            </button>
          </div>
        </div>
      </div>
    </div>
    <br>
  </div>
</template>

<script>
import {mapActions} from 'vuex'

export default {
  props: ['stock'],
  data(){
    return {
      quantity: 0
    }
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity
    }
  },
  methods:{
    ...mapActions({
      placeSellOrder: 'sellStock'
    }),
    sellStock(){
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      }
      this.placeSellOrder(order)
      this.quantity = 0
    }
  }
}
</script>

<style lang="css" scoped>
  .danger{
    border: 1px solid red;
  }
</style>
