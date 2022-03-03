<template>
  <section id="products" class="products">
    <div class="container">
      <div v-if="products" class="pb-5 cont justify-content-center">
        <div class="row col-lg-12 proji" style="row-gap: 30px">
          <div
            v-for="product in products"
            :key="product._id"
            class="col-lg-3 col-md-6"
            style="display: flex; justify-content: center"
          >
            <div class="card shadow ani-card" style="width: 18rem">
              <img
                :src="product.product_image"
                class="card-img-top"
                alt="..."
              />
              <div class="card-body">
                <h4 class="card-title text-black">
                  {{ product.product_name }}
                </h4>
                <p class="card-text text-black">R{{ product.product_price }}</p>
              </div>

              <div class="card-body text-center">
                <input
                  type="number"
                  min="1"
                  value="1"
                  id="addToCartt${position}"
                  style="
                    width: 40px;
                    padding-bottom: 7px;
                    border-radius: 3px;
                    height: 37px;
                  "
                />
                <button
                  type="button"
                  class="btn mx-2 border-dark card-btn"
                  @click="addToCart(index)"
                >
                  <i class="bi bi-cart2"></i>
                </button>
                <button
                  type="button"
                  class="btn border-dark card-btn"
                  data-bs-toggle="modal"
                  data-bs-target="#updateModal"
                >
                  <i class="bi bi-pencil-square"></i>
                </button>
                <button
                  type="button"
                  class="btn border-dark mx-2 card-btn"
                  @click.prevent="deleteProduct(product._id)"
                >
                  <i class="bi bi-trash3"></i>
                </button>
                <!-- update modal -->
              </div>

              <div
                class="modal fade"
                id="updateModal"
                tabindex="-1"
                aria-labelledby="exampleModalLabel"
                aria-hidden="true"
              >
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h5 class="modal-title" id="exampleModalLabel">
                        Update {{ product._id }}
                      </h5>
                      <button
                        type="button"
                        class="btn-close"
                        data-bs-dismiss="modal"
                        aria-label="Close"
                      ></button>
                    </div>
                    <div class="modal-body">
                      <div class="mb-3">
                        <label for="editTitle${position}" class="form-label"
                          >Name</label
                        >
                        <input
                          class="form-control"
                          type="text"
                          name="editTitle${position}"
                          id="editTitle${position}"
                          v-model="product.product_name"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="editCategory${position}" class="form-label"
                          >Price</label
                        >
                        <input
                          class="form-control"
                          type="text"
                          name="editPrice${position}"
                          id="editPrice${position}"
                          v-model="product.product_price"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="editPrice${position}" class="form-label"
                          >Category</label
                        >
                        <input
                          class="form-control"
                          type="text"
                          name="editPrice${position}"
                          id="editPrice${position}"
                          v-model="product.product_category"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="editImg${position}" class="form-label"
                          >Image URL</label
                        >
                        <input
                          class="form-control"
                          type="text"
                          name="editImg${position}"
                          id="editImg${position}"
                          v-model="product.product_image"
                        />
                      </div>
                    </div>
                    <div class="modal-footer">
                      <button
                        type="button"
                        class="btn btn-secondary"
                        data-bs-dismiss="modal"
                      >
                        Close
                      </button>
                      <button
                        type="button"
                        class="btn btn-primary"
                        data-bs-dismiss="modal"
                        @:click="updateProduct(_id)"
                      >
                        Save changes
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="loading" v-else></div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      products: null,
    };
  },
  // GETTING USER
  mounted() {
    if (localStorage.getItem("jwt")) {
      fetch("https://groupapibackend.herokuapp.com/products/", {
        method: "GET",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.products = json;
          console.log(json);
          this.products.forEach(async (product) => {
            await fetch(
              "https://groupapibackend.herokuapp.com/users" +
                product.created_by,
              {
                method: "GET",
                headers: {
                  "Content-type": "application/json; charset=UTF-8",
                  Authorization: `Bearer ${localStorage.getItem("jwt")}`,
                },
              }
            )
              .then((response) => response.json())
              .then((json) => {
                product.created_by = json.user_name;
              });
          });
        })
        .catch((err) => {
          alert("User not logged in");
        });
    } else {
      alert("User not logged in");
      this.$router.push({ name: "Login" });
    }
  },

  methods: {
    // UPDATE ONE PRODUCTS(not done)

    updateProduct(_id) {
      fetch("https://groupapibackend.herokuapp.com/products" + this._id, {
        method: "PUT",
        body: JSON.stringify({
          product_name: this.product_name,
          product_price: this.product_price,
          product_category: this.product_category,
          product_image: this.product_image,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("Product Created");
          this.$router.push({ name: "Products" });
        })
        .catch((err) => {
          alert(err);
        });
      console.log(updateProduct(_id));
    },

    // DELETE PRODUCT(done)
    deleteProduct(id) {
      const config = {
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      };
      let apiURL = `https://groupapibackend.herokuapp.com/products/${id}`;

      let indexOfArrayItem = this.products.findIndex((i) => i._id === id);

      if (window.confirm("Do you really want to delete?")) {
        axios
          .delete(apiURL, config)
          .then(() => {
            this.products.splice(indexOfArrayItem, 1);
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },

  },
};
</script>

<style>
.card-img-top {
  border-radius: 10px;
  height: 200px;
  object-fit: cover;
}
</style>
