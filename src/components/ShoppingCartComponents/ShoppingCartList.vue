<template>
  <section>
    <shoppingCartItem class="mt-5" :shoppingCartItems="shoppingCartItems" v-if="shoppingCartItems.length > 0"></shoppingCartItem>
    <h4 class="mt-5 shoppingCartEmptyText text-center" v-else>No Items</h4>
    
    <!-- Divider -->
    <div class="divider mt-5 mb-4"></div>

    <!-- Total Price -->
    <div class="shoppingCartTotalPrice d-sm-flex d-block justify-content-end" v-if="shoppingCartItems.length > 0">
      <h1>Total: {{totalPrice}}€</h1>
      <div class="buyItemsBtn d-block btn btn-lg btn-success align-self-center">Buy</div>
    </div>
  </section>
</template>
  
  <script>
import shoppingCartItem from "@/components/ShoppingCartComponents/ShoppingCartItem.vue"

export default {
  name: "ShoppingCartList",

  props: {
    shoppingCartItems: [],
  },

  components: {
    shoppingCartItem,
  },

  data() {
    return {
      totalPrice: 0,
    }
  },

  methods: {
    calcTotalPrice() {
      this.shoppingCartItems.forEach(e => {
        this.totalPrice += e.price;
      });
      this.totalPrice = Math.ceil(this.totalPrice);
    },

    removeFromShoppingCart(productItem) {
      this.shoppingCartItems.splice(this.shoppingCartItems.findIndex((obj) => obj.id === productItem.id), 1);
    }
  },

  mounted() {
    this.calcTotalPrice();
  },

  watch: {
    shoppingCartItems(e) { // Watch if shoppingCartItems Arry is changing in length
      let tempTotalPrice = 0;

      e.forEach(i => {
        tempTotalPrice += i.price;
      });

      return this.totalPrice = Math.ceil(tempTotalPrice);
    }
  }
  
};
</script>
  
<style scoped>
.shoppingCartEmptyText {
  font-size: 25px;
  font-weight: 400;
}

/* Divider */
.divider {
  background: rgb(197, 197, 197);
  height: 1px;
}

/* Total Shopping Price text */
.shoppingCartTotalPrice h1 {
  text-align: right;
  font-size: 30px;
  margin-right: 10px;
  font-weight: 400;
  margin-bottom: 20px;
}

.shoppingCartTotalPrice .buyItemsBtn {
  margin-left: 0;
}


/* Responsive */
@media (min-width: 576px) { /* 576px */
  .shoppingCartTotalPrice h1 {
    font-size: 35px;
    margin-right: 10px;
    margin-bottom: 0;
    text-align: left;
    font-weight: 400;
  }
  .shoppingCartTotalPrice .buyItemsBtn {
    margin-left: 30px;
  }
}
</style>
  