<template>
  <div>
    <!-- ReturnBTN Normal-->
    <div class="d-none d-lg-block btn btn-primary rounded-pill linkToHomeView" @click="linkToHomeView">
      <i class="fas fa-arrow-left"></i>
    </div>

    <!-- ReturnBTN Responsive -->
    <div class="d-lg-none d-block d-sm-inline-block btn btn-primary linkToHomeViewResponsive" @click="linkToHomeView">
      <i class="fas fa-arrow-left"></i>
      <p class="d-inline-block">Return Product List</p>
    </div>

    <!-- Shopping Cart Header --> 
    <div class="shoppingCartViewHeader mt-4">
      <h1>Shopping Cart</h1>
    </div>

    <!-- Shopping Cart List Component -->
    <ShoppingCartList :shoppingCartItems="shoppingCartItems"></ShoppingCartList>
  </div>
</template>

<script>
import ShoppingCartList from "@/components/ShoppingCartComponents/ShoppingCartList.vue"

export default {
  name: 'ShoppingCartView',

  props: {
    shoppingCartItems: []
  },

  components: {
    ShoppingCartList,
  },

  methods: {
    linkToHomeView() {
     this.$router.replace({ path: '/' })
    }
  }
}
</script>

<style scoped>
.shoppingCartViewHeader {
  margin-top: 10px;
}
.shoppingCartViewHeader h1 {
  font-size: 30px;
}

.linkToHomeView {
  position: fixed;
  top: 3%;
  left: 2%;
}

.linkToHomeViewResponsive {
  margin-top: 20px;
  width: auto;
}
.linkToHomeViewResponsive i {
  margin-right: 20px;
}
</style>
