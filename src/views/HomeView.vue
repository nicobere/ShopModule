<template>
    <div class="my-4">
      <ProductList></ProductList>
    </div>
</template>

<script>

import ProductList from '@/components/HomeComponents/ProductList.vue';

export default {
  name: 'HomeView',

  components: {
    ProductList
  }
}
</script>
