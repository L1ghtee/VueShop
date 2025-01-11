<template>
  <div class="products-list">
    <div class="product" v-for="product in store.products" :key="product.id" @click="goToProductPage(product.id)">
      <img class="product-image" :src="product.thumbnail" alt="">
      <div class="product-txt">
        <h2>Brand: {{ product.brand }} </h2>
        <p><b>Description:</b> {{ product.description }}</p>
        <p><b>Price:</b> ${{ product.price }}</p>

      </div>

    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
export default defineComponent({
  name: "CatalogView",
});
</script>

<script setup>
import { onMounted } from 'vue';
import { productsStore } from "@/stores/products";
import { useRouter } from 'vue-router';

const store = productsStore();
const router = useRouter();
const goToProductPage = (id) => {
  router.push({ name: 'ProducView', params: { id } })
}
onMounted(async () => {
  await store.fetchProductsFromDB()

})
</script>
<style scoped>
.products-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.product {
  padding: 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
  cursor: pointer;
}

.product-image {
  object-fit: cover;
}

.product-txt {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
