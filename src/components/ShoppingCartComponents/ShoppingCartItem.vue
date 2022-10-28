<template>
  <section>
    <article class="shoppingCartItemBox shadow-sm" v-for="(item, index) in shoppingCartItems" :key="index">
      <div class="row h-100 d-flex align-items-center">

        <!-- Article Image -->
        <div class="col-1 align-self-center">
          <div class="shoppingCartItemImage">
            <img :src="item.image" :alt="item.title">
          </div>
        </div>

        <!-- Article Title -->
        <div class="col-6 col-sm-8">
          <div class="shoppingCartItemTitle">
            <h2>{{item.title}}</h2>
          </div>
        </div>

        <!-- Article Price -->
        <div class="col-3 col-sm-2 align-self-center ">
          <h3 class="m-0 shoppingCartItemPrice">€ {{Math.ceil(item.price)}}</h3>
        </div>

        <!-- Remove from Shopping Cart -->
        <div class="col-1 shoppingCartItemRemove" @click="removeFromShoppingCart(item)">
          <i class="fas fa-trash-alt text-danger"></i>
        </div>
      </div>
    </article>
  </section>
</template>
  
<script>
export default {
  name: "ShoppingCartItem",

  props: {
    shoppingCartItems: []
  },

  methods: {
    removeFromShoppingCart(productItem) {
      this.$parent.removeFromShoppingCart(productItem);
    }
  }
};
</script>
  
<style scoped>
/* Shopping Cart Item Box */
.shoppingCartItemBox {
  background: rgb(255, 255, 255);
  height: 118px;
  padding: 0 20px;
}
.shoppingCartItemBox:not(:last-child) {
  margin-bottom: 10px;
}

.shoppingCartItemBox .shoppingCartItemImage img {
  max-width: 45px;
  user-select: none;
}
.shoppingCartItemBox .shoppingCartItemTitle h2 {
  font-size: 15px;
  margin: 0 10px 0 30px;
  font-weight: 400;
  width: 150px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.shoppingCartItemBox .shoppingCartItemRemove i {
  width: auto;
  cursor: pointer;
  font-size: 19px;
  padding: 8px;
}
.shoppingCartItemBox .shoppingCartItemRemove i:hover {
  border: 1px solid #dc3545;
  border-radius: 50px;
}

.shoppingCartItemPrice {
  font-size: 19px;
  font-weight: 400;
}


/* Responsive */
@media (min-width: 300px) { /* 300px */
  .shoppingCartItemBox .shoppingCartItemTitle h2 {
    width: 120px;
  }
}

@media (min-width: 576px) { /* 576px */
  .shoppingCartItemBox {
    /* border-radius: 100px; */
    border: 1px solid rgb(230, 230, 230);
    padding: 15px 50px;
  }
  .shoppingCartItemBox .shoppingCartItemImage img {
    max-width: 45px;
    user-select: none;
  }
  .shoppingCartItemBox .shoppingCartItemTitle h2 {
    font-size: 17px;
    width: auto;
  }
  .shoppingCartItemBox .shoppingCartItemRemove i {
    font-size: 25px;
  }
  .shoppingCartItemPrice {
    font-size: 20px;
  }
}

@media (min-width: 768px) { /* 768px */
  .shoppingCartItemBox .shoppingCartItemImage img {
    max-width: 50px;
    user-select: none;
  }
  .shoppingCartItemBox .shoppingCartItemTitle h2 {
    font-size: 17px;
  }
  .shoppingCartItemBox .shoppingCartItemRemove i {
    font-size: 25px;
  }
  .shoppingCartItemPrice {
    font-size: 25px;
  }
}

@media (min-width: 900px) { /* 900px */
  .shoppingCartItemBox .shoppingCartItemTitle h2 {
    font-size: 19px;
  }
  .shoppingCartItemBox .shoppingCartItemRemove i {
    font-size: 25px;
  }
  .shoppingCartItemPrice {
    font-size: 25px;
  }
}

@media (min-width: 1500px) { /* 1500px */
  .shoppingCartItemBox .shoppingCartItemTitle h2 {
    font-size: 23px;
  }
  .shoppingCartItemBox .shoppingCartItemRemove i {
    font-size: 25px;
  }
  .shoppingCartItemPrice {
    font-size: 25px;
  }
}
</style>
  