<template>
  <article :id="'article_' + productItem.id" class="productItem shadow">
    <div class="productItemContent">

      <!-- Item Star Rating -->
      <div class="itemRating d-flex shadow-sm">
        <div class="itemRatingStars d-flex justify-content-between">
          <span class="text-warning" v-for="(item, index) in roundUpValue(productItem.rating.rate)" :key="index"><i class="fas fa-star"></i></span>
        </div>
      </div>
   
      <!-- Item Image & Item Title -->
      <div class="position-relative d-flex flex-wrap align-items-center h-100 justify-content-center">
        <figure class="my-3">
          <img :src="productItem.image" v-if="productItem.image != ''"/> 
          <img :src="'https://media.istockphoto.com/id/1409329028/vector/no-picture-available-placeholder-thumbnail-icon-illustration-design.jpg?s=612x612&w=0&k=20&c=_zOuJu755g2eEUioiOUdz_mHKJQJn-tDgIAhQzyeKUQ='" style="max-width: 45%;" v-else /> 
        </figure>
        <h1 class="productItemTitle">{{productItem.title}}</h1>
      </div>
    </div>

    <!-- Bottom Divider -->
    <div class="contentDividerLine mt-5 mb-3"></div>

    <!-- Bottom Content -->
    <div class="d-flex justify-content-between">
      <div class="itemPrice">
        <p>€ {{roundUpValue(productItem.price)}}</p>
      </div>

      <div class="d-flex">
        <!-- If Item is already in Shopping Cart -->
        <div class="deleteItem btn btn-sm btn-outline-danger d-flex align-items-center" @click="deleteItemFromList(productItem)">
          <span>Delete</span>
          <i class="fas fa-trash-alt"></i>
        </div>

        <!-- Item Add / Remove Cart Button -->
        <div class="itemToCart btn btn-sm btn-outline-primary d-flex align-items-center" v-if="!isInShoppingCart" @click="addItemToShoppingCart(productItem)">
          <span>Add</span>
          <i class="fas fa-shopping-cart"></i>
        </div>
        <div class="itemToCart btn btn-sm btn-outline-danger d-flex align-items-center" v-else @click="removeItemFromShoppingCart(productItem)">
          <span>Remove</span>
          <i class="fas fa-minus"></i>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
import axios from 'axios';

export default {
  name: "ProductListItem",
  props: {
    productItem: [],
  },

  data() {
     return {
      isInShoppingCart: false,
     }
  },

  methods: {
    roundUpValue(item) {
      return Math.ceil(item);
    },

    deleteItemFromList(productItem) {
      this.$parent.deleteItemFromList(productItem);
    },

    // Call Parent Func AddToCart
    addItemToShoppingCart(productItem) {
      this.$parent.addItemToShoppingCart(productItem);
      this.isInShoppingCart = true;
    },
    // Call Parent Function RemoveFromCart
    removeItemFromShoppingCart(productItem) {
      this.$parent.removeItemFromShoppingCart(productItem);
      this.isInShoppingCart = false;
    },
  },
};

// onstock value checken mit product rating count

</script>

<style scoped>

/*  Product Item  */
.productItem {
  width: 100%;
  background: white;
  min-height: 220px;
  padding: 10px;
  border-radius: 10px;
  transition: all 0.1s;
  border: 2px solid white;
  position: relative;
}

.productItem:hover {
  transform: scale(1.03);
  cursor: pointer;
  border: 2px solid var(--mainColor);
}

.productItem .itemPrice {
  font-size: 24px;
  font-weight: 500;
  margin-left: 10px;
}

.productItem .itemToCart i {
  margin-left: 5px;
}
.productItem .itemToCart:hover {
  color: #fff;
}

.productItem .deleteItem {
  margin-right: 10px;
}
.productItem .deleteItem i {
  margin-left: 5px;
}
.productItem .deleteItem:hover {
  color: #fff;
}

/*  Product Item Content  */
.productItemContent {
  height: 180px;
  text-align: center;
}

.productItemContent .itemRating {
  background: #fff;
  border: 1px solid rgb(228, 228, 228);
  border-radius: 50px;
  position: absolute;
  top: -10px;
  right: 20px;
  padding: 3px 10px;
  text-align: center;
}

.productItemContent img {
  max-width: 10%;
  user-select: none;
}
.productItemContent .productItemTitle {
  position: absolute;
  top: 180px;
}
.productItemContent h1 {
  font-size: 18px;
  text-align: center;
}


/*  Item Content Divider  */
.contentDividerLine {
  width: 100%;
  height: 1px;
  background: rgb(235, 235, 235);
}

@media (min-width: 375px) { /* 375px */
  .productItemContent img {
    max-width: 20%;
  }
}

@media (min-width: 576px) { /* 576px */
  .productItemContent img {
    max-width: 13%;
  }
}

@media (min-width: 768px) { /* 768px */
  .productItemContent img {
    max-width: 10%;
  }
}

@media (min-width: 992px) { /* 992px */
  .productItem {
    width: 47%;
    margin-right: 20px;
  }

  .productItemContent img {
    max-width: 15%;
  }
}

@media (min-width: 1250px) { /* 1250px */
  .productItem {
    width: 48%;
    margin-right: 20px;
  }
}

@media (min-width: 1800px) { /* 1800px */
  .productItem {
    width: 32%;
  }
}

</style>