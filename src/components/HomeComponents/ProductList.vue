<template>
  <section>
    <div class="d-block d-sm-flex">
      <!-- Select Category Input -->
      <select class="selectCategoryInput form-select" aria-label="Default select example" @change="selectCategory($event)">
        <option value="all categories">All Categories</option>
        <option v-for="(item, index) in categoryList" :key="index" :value="item" class="text-capitalize">{{item}}</option>
      </select>

      <!-- Responsive Shopping Cart  -->
      <div class="shoppingCartBtnResponsive d-xl-none d-block d-sm-inline-block mt-2 mt-sm-0 btn btn-primary" @click="linkToShoppingCartView">
        <span>Shopping Cart - {{shoppingCartList.length}}</span>
      </div>

      <!-- Add Product BTN  -->
      <div class="addProductBtn d-block d-sm-inline-block mt-3 mt-sm-0 btn btn-success" @click="openModalAddProduct">
        Add New Product <i class="fas fa-plus"></i>
      </div>

      <!-- Shopping Cart Normal -->
      <div class="shoppingCartBtn d-none d-xl-flex btn btn-primary text-white" @click="linkToShoppingCartView">
        <i class="fas fa-shopping-cart"></i>
        <span>{{shoppingCartList.length}}</span>
      </div>

    </div>

    <!-- Current Category Filter Text -->
    <div class="mt-3">
      <div class="currentCategoryFilterHeader" v-show="currentCategoryFilter != ''">
        <i class="fas fa-filter text-primary"></i>
        <h5 class="d-inline-block">Filter:</h5>
        <span class="currentCategoryFilterText alert alert-primary py-1 px-2">{{currentCategoryFilter}}</span>
      </div>
    </div>
    
    <!-- Product Item Component-->
    <div id="productList" class="mt-5 d-block d-sm-flex flex-wrap">
      <ProductListItem v-for="(item, index) in productList" :key="index" :productItem="item" class="mb-4"></ProductListItem>
    </div>

    <!-- Modal Add Product -->
    <openModalAddProduct></openModalAddProduct>

  </section>
</template>

<script>
import ProductListItem from "@/components/HomeComponents/ProductListItem.vue";
import openModalAddProduct from "./modalAddProduct.vue"
import axios from "axios";
import "jquery"

export default {
  name: "ProductList",

  components: {
    ProductListItem,
    openModalAddProduct,
  },

  props: {},

  data() {
    return {
      productList: [], // Getted List with Product Items
      
      categoryList: [], // Getted List with all Categories
      currentCategoryFilter: "",

      shoppingCartList: [], // Local Shopping Cart List
    };
  },

  methods: {
    // Get all Product Items
    getProducts() {
      axios.get("https://fakestoreapi.com/products")
        .then((res) => { this.productList = res.data; })
        .catch((err) => console.log(err));
    },

    // Get Product Categories
    getCategories() {
      axios.get("https://fakestoreapi.com/products/categories")
        .then((res) => { this.categoryList = res.data; })
        .catch((err) => console.log(err));
    },

    // Get Filtered Product List by Category
    selectCategory(event) {
      this.currentCategoryFilter = event.target.value

      if(event.target.value != "all categories") {
        axios.get("https://fakestoreapi.com/products/category/" + event.target.value)
        .then(res => { this.productList = res.data; })
        .catch(err => console.log(err))
      }
      else { // Else for "All Categories"
        this.getProducts();
        this.currentCategoryFilter = ""; // Reset Filter Text
      }
    },

    // Add Item to Cart
    addItemToShoppingCart(productItem) {
      this.shoppingCartList.push(productItem);
    },

    // Remove Item from Cart by ID
    removeItemFroMShoppingCart(productItem) {
      if(this.shoppingCartList.length > 0) {
        this.shoppingCartList.splice(this.shoppingCartList.findIndex((obj) => obj.id === productItem.id), 1);
      }
    },

    deleteItemFromList(productItem) {
      axios.delete("https://fakestoreapi.com/products/" + productItem.id, {method:"DELETE"})
      .then(res => {
        this.productList.splice(this.productList.findIndex((obj) => obj.id === productItem.id), 1);
      })
      .catch(err => console.log(err))
    },

    linkToShoppingCartView() {
      let shoppingCartItems = this.shoppingCartList;
      this.$router.push({name:'ShoppingCartView', params:{shoppingCartItems}});
    },

    // Open Product Modal
    openModalAddProduct() {
      openModalAddProduct.methods.openModalAddProduct(); // Access Methods from Vue FIle openModalAddProduct
    },
  },

  created() {
    this.getProducts();
    this.getCategories();
  },
};
</script>

<style scoped>
section {
  position: relative;
}

.selectCategoryInput {
  width: 100%;
}

.addProductBtn {
  margin-left: 0;
}
.addProductBtn i {
  margin-left: 5px;
}

/* ShoppingCart Btn Normal */
.shoppingCartBtn {
  position: fixed;
  right: 3%;
  bottom: 5%;
  align-items: center;
  padding: 12px;
  border-radius: 50px;
  transition: all ease-in-out 0.1s;
}
.shoppingCartBtn:hover {
  transform: scale(1.05);
  cursor: pointer;
}
.shoppingCartBtn i {
  font-size: 20px;
  margin: 0 15px 0 5px;
}

.shoppingCartBtn span {
  font-size: 20px;
  margin-right: 13px;
}

.shoppingCartBtnResponsive {  /* Responsive View of ShoppingCart*/
  margin-left: 0;
}

.currentCategoryFilterHeader i {
  font-size: 19px;
  margin-right: 5px;
}
.currentCategoryFilterHeader h5 {
  font-size: 19px;
}

.currentCategoryFilterText {
  text-transform: capitalize;
  margin-left: 10px;
  font-size: 18px;
  font-weight: 500;
}

/* Responsive */
@media (min-width: 576px) { /* 576px */
  .selectCategoryInput {
    width: 49%;
  }
  .addProductBtn {
    margin-left: 20px;
    width: 49%;
  }

  .shoppingCartBtnResponsive {
    margin-left: 15px;
  }
}

@media (min-width: 768px) { /* 768px */
  .selectCategoryInput {
    width: 30%;
  }
  .addProductBtn {
    margin-left: 20px;
    width: auto;
  }
}

@media (min-width: 992px) { /* 992px */
  .selectCategoryInput {
    width: 25%;
  }
}

@media (min-width: 1400px) { /* 1400px */
  .selectCategoryInput {
    width: 15%;
  }
}
</style>
