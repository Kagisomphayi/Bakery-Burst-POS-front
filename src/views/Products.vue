<template>
  <!-- projects section -->
  <section id="projects" class="products">
    <div class="container hr">
      <hr class="bg-white" />
    </div>
    <div class="container">
      <div class="pb-5 justify-content-center">
        <h1 class="text-center display-6 mb-5 fw-bold subtitlee"><u>Products</u></h1>
        <div class="row col-lg-12 proji" style="row-gap: 30px">
          <div
            v-for="project of projects"
            :key="project.title"
            class="col-lg-3 col-md-6"
            style="display: flex; justify-content: center"
          >
            <div class="card shadow ani-card" style="width: 18rem">
              <img :src="project" class="card-img-top" alt="..." />
              <div class="card-body">
                <h4 class="card-title text-black">{{ project.title }}</h4>
                <p class="card-text text-black">{{ project.description }}</p>

              </div>

              <div class="card-body text-center">
                <input type="number"  min=1 value=1 id="addToCartt${position}" style="width:35px; height:37px;">
                <button
                  type="button"
                  class="btn mx-2  card-btn btn-success"
                  onclick="addtocart(${position})"
                >
                  <i class="bi bi-cart2"></i>
                </button>
                <button
                  type="button"
                  class="btn card-btn  btn-primary"
                  data-bs-toggle="modal"
                  data-bs-target="#editProduct${position}"
                >
                  <i class="bi bi-pencil-square"></i>
                </button>
                <button
                  type="button"
                  class="btn mx-2 card-btn btn-danger "
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
    <div class="container hr">
      <hr class="bg-white" />
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      projects: null,
    };
  },

  mounted() {
    fetch("https://kagisomphayiportfolio.herokuapp.com/projects")
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        this.projects = data;
      });
  },

  methods: {
    addToCart(product) {
      this.$emit("addToCart", product);
    },
  },
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
