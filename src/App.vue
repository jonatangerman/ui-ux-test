<script setup>
import ProductCard from './components/ProductCard.vue';
import { ref } from 'vue';

const products = ref([]);
const skip = ref(0);
const total = ref(null);
const skipNumber = 30;

async function getData() {
  const response = await fetch(`https://dummyjson.com/products?skip=${skip.value}`, {
    method:'get',
  }).then((data) => {
    return data.json();
  }).then((data) => {
    return data;
  })

  products.value = [...products.value, ...response.products];
  total.value = response.total;
}

function loadMore() {
  skip.value = skip.value + skipNumber;
  getData();
}

getData();
</script>

<template>
  <main>
    <template v-if="products.length > 0">
      <ul id="main-list">
        <transition-group name="fade">
          <ProductCard :product="product" :key="product.id" v-for="product in products" />
        </transition-group>
      </ul>
      <button v-if="products.length !== total" @click="loadMore">Load More</button>
    </template>
    <img id="loader" v-else src="/loader.gif"/> 
  </main>
    
</template>

<style scoped>
main {
  padding: 10px;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  flex-direction: column;
  position: relative;
}

#loader {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100px;
}

ul#main-list {
  margin: 0;
  padding: 0;
  width: 100%;
  gap: 10px;
  display:flex;
  flex-wrap: wrap;
  list-style: none;
  margin-bottom: 30px;
}

button {
  padding: 20px 40px;
  width: fit-content;
  background-color: transparent;
  border: 1px solid gray;
  color: gray;
  margin-bottom: 20px;
}

button:hover {
  background-color: gray;
  color: black;
  cursor: pointer;
}



</style>
