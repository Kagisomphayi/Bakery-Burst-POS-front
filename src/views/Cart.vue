<template>
  <!-- <div>
    <h1>Your Cart</h1>
    <div class="products">
      <div v-for="(projects, index) in cart" :key="index">
        <h3>{{product.name}}</h3>
        <img :src="product.image" />
        <div>{{product.cost}}</div>
        <button v-on:click="deleteFromCart(projects)">Remove from cart</button>
      </div>
    </div>
  </div> -->

      <div class="container">
      <div class="pb-5 justify-content-center">
        <h1 class="text-center display-6 mb-5 fw-bold subtitlee"><u>Products</u></h1>
        <div class="row col-lg-12 proji" style="row-gap: 30px">
          <div
            v-for="product of products"
            :key="product.name"
            class="col-lg-3 col-md-6"
            style="display: flex; justify-content: center"
          >
            <div class="card shadow ani-card" style="width: 18rem">
              <img :src="product.image" class="card-img-top" alt="..." />
              <div class="card-body">
                <h4 class="card-title text-black">{{ product.name }}</h4>
                <p class="card-text text-black">{{ product.cost }}</p>
              </div>

              <div class="card-body text-center">
                <input type="number"  min=1 value=1 id="addToCartt${position}" style="width:35px; height:37px;">
                <button
                  type="button"
                  class="btn mx-2 card-btn btn-danger"
                  onclick="deleteProduct(${position})"
                >
                 <i class="bi bi-trash3"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
export default {

  data: () => {
    return {
      cart: []
    };
  },
  props: ["cart"],
  methods: {
    deleteFromCart(product) {
      this.$emit("removeItemFromCart", product);
    },
    removeItemFromCart(product) {
      this.cart.splice(this.cart.indexOf(product), 1);
    },
  }
};
</script>

<style scoped>
.products {
  padding-top: 50px;
}
.card{
  border-radius: 10px;
}
.subtitlee{
  margin-top:70px ;
}
.card-img-top{
    border-radius: 10px;
}
</style>