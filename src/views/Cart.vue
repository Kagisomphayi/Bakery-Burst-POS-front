<template>
  <div>
    <h1>Your Cart</h1>
    <div class="products">
      <div v-for="(product, index) in cart" :key="index">
        <h3>{{product.name}}</h3>
        <img :src="product.image" />
        <div>{{product.cost}}</div>
        <button v-on:click="deleteFromCart(product)">Remove from cart</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["cart"],
  methods: {
    deleteFromCart(product) {
      this.$emit("removeItemFromCart", product);
    }
  }
};
</script>

<style>
</style>