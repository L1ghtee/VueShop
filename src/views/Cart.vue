<template>
  <button @click="router.push({ name: 'Catalog'})">Back to catalog</button>
  <div v-if="!store.cart.length">
    <h1>Empty Cart...</h1>

  </div>

  <div class="cart-items" v-else>
    <h1>Cart</h1>
    <div class="cart-item" v-for="item in store.cart" :key = "item.id">
      <div class="item-details">
        <img :src="item.thumbnail" alt="">
        <span>Brand: {{item.brand}}</span>
        <span>Category: {{item.category}}</span>
        <span>Price: ${{item.price}}</span>
        <button @click="removeFromCart(item.id)">Remove</button>
      </div>
    </div>
  </div>
</template>

<script>
  import { defineComponent } from "vue";
  export default defineComponent({
   name: "CartView",
});
</script>
<script setup>
  import { productsStore } from "@/stores/products";
  import { useRouter } from 'vue-router';
  const router = useRouter();
  const store = productsStore();
  const removeFromCart = (id) => {
    store.removeFromCart(id);
  }
</script>
