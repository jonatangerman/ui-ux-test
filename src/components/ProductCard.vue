<script setup>
import { defineProps, computed } from 'vue';

const props = defineProps({
  product: {
    type: Object,
    required: true
  }
});

const discount = computed(() => {
  return (props.product.price * (100 - props.product.discountPercentage ) / 100).toFixed(2);
});

</script>

<template>
  <li>
      <div class="img-container"><img :src="product.images[product.images.length-1]"/></div>
      <div class="content-container">
        <div class="title-container">
          <a href="javascript:void(0);">{{ product.title }}</a>({{ product.rating }})
        </div>
        <p v-if="product.discountPercentage">
          <span class="original-price">{{ product.price }} usd</span><span class="price">{{ discount }} usd</span> <span class="discount-percentage"> ({{product.discountPercentage}}%) off</span>
        </p>
        <p v-else>
          <span class="price">{{ product.price }}</span>
        </p>
        <p class="description">{{ product.description }}</p>
      </div>
    </li>
</template>

<style scoped>
.content-container {
  padding: 10px;
}

a {
  font-size: 16px;
  color: lightblue;
}

.title-container {
  font-size: 10px;
}

.content-container span, .content-container a {
  margin-right: 5px;
}

li { 
  width: calc(25% - 10px);
  border: 1px solid gray;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.img-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 200px;
  overflow: hidden;
}

li img {
  width: 100%;
  object-fit: cover;
}

.discount-percentage {
  font-size: 12px;
}

.original-price {
  font-size: 13px;
  text-decoration: line-through;
}

.price {
  font-weight: bold;
}

.description {
  font-size: 13px;
}

@media (max-width: 756px) {
  li { 
    width: calc(50% - 10px);
  }

  .img-container { 
    height: 150px;
  }
}

@media (max-width: 350px ) {
  li { 
    width: 100%;
  }

  li img {
    height: 100%;
  }

  .img-container {
    height: auto;
  }

}
</style>
