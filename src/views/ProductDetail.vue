<template>
  <button @click="router.push({ name: 'Catalog'})">Back to catalog</button>
 <div class="product">
  <div class="product-image">
    <img :src="selectedProduct.thumbnail" alt="">
  </div>
  <div class="product-details">
        <h1>{{ selectedProduct.name }}</h1>
        <h2>Brand: {{ selectedProduct.brand }} </h2>
        <p><b>Description:</b> {{ selectedProduct.description }}</p>
        <p><b>Price:</b> ${{ selectedProduct.price }}</p>
         <button @click="addToCart" >Add to cart</button>
  </div>
 </div>
</template>

<script>
  import { defineComponent } from "vue";
  export default defineComponent({
    name: "ProductDetail",
  });
</script>

<script setup>
import { computed } from 'vue';
import { productsStore } from "@/stores/products";
import { useRoute, useRouter } from 'vue-router';

const store = productsStore();
const router = useRouter();
const route = useRoute();

const selectedProduct = computed(() => {
   return store.products.find((item)=> item.id === Number(route.params.id))
})


const addToCart = () => {
  store.addToCart(selectedProduct.value);
  router.push({ name: 'CartView' })
}

</script>
