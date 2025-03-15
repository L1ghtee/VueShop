<template>
  <header>
    <nav>
      <div class="cart-items" @click="router.push({ name: 'CartView' })">
        <p>Items in cart: {{ store.cart.length }}</p>
      </div>
    </nav>
  </header>
  <main>
    <RouterView />
  </main>
</template>

<script setup>
import { useRouter } from 'vue-router';
import { productsStore } from "@/stores/products";

const router = useRouter();
const store = productsStore();
</script>

<style scoped>
.cart-items {
  cursor: pointer;
  padding: 10px;
  background-color: #f8f8f8;
  border-radius: 5px;
}
</style>
