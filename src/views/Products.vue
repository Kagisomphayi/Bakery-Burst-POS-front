<template>
  <!-- projects section -->
  <section id="products" class="products">
    <div class="container">
      <div v-if="products" class="pb-5 cont justify-content-center">
        <h1 class="text-center display-6 mb-5 fw-bold subtitlee">
          <u>Products</u>
        </h1>
        <div style="display: flex; justify-content: center">
          <div class="sort">
            <div class="sort-content">
              <h6 class="mb-0">SortByPrice:</h6>
              <select
                class="form-select text-center"
                name=""
                id="sortPrice"
                onchange="sortPrice()"
              >
                <option value="ascending">Ascending</option>
                <option value="descending">Descending</option>
              </select>
              <h6>SortByTitle:</h6>
              <select
                class="form-select text-center"
                name=""
                id="sortTitle"
                onchange="sortTitle()"
              >
                <option value="ascending">Ascending</option>
                <option value="descending">Descending</option>
              </select>

              <!-- Button trigger modal -->
              <button
                type="button"
                class="btn mt-4 button-body"
                data-bs-toggle="modal"
                data-bs-target="#addProductModal"
              >
                <p class="sub">Add a product</p>
              </button>

              <!-- Modal -->
              <div
                class="modal fade"
                id="addProductModal"
                tabindex="-1"
                aria-labelledby="exampleModalLabel"
                aria-hidden="true"
              >
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h5 class="modal-title" id="exampleModalLabel">
                        Add product
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
                        <label for="addTitle" class="form-label">Name</label>
                        <input
                          class="form-control"
                          type="text"
                          name="addName"
                          id="addName"
                          v-model="product_name"
                        />
                      </div>
                      <div class="mb-3">
                        <label class="form-label">Category</label>
                        <select
                          class="form-select"
                          name="addCategory"
                          id="addCategory"
                          v-model="product_category"
                        >
                          <option value="Shoes">Cakes</option>
                          <option value="Accessories">Cookies</option>
                          <option value="Clothing">Bread</option>
                        </select>
                      </div>
                      <div class="mb-3">
                        <label for="addPrice" class="form-label">Price</label>
                        <input
                          class="form-control"
                          type="text"
                          name="addPrice"
                          id="addPrice"
                          v-model="product_price"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="addImg" class="form-label">Image</label>
                        <input
                          class="form-control"
                          type="text"
                          name="addImg"
                          id="addImg"
                          v-model="product_image"
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
                        :onclick="createProduct()"
                      >
                        Create Product
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="row col-lg-12 proji" style="row-gap: 30px">
          <div
            v-for="(product, product_id) in products"
            :key="product_id"
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
                <p class="card-text text-black">{{ product._id }}</p>
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
                  v-on:click="addToCart(index)"
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
                  v-on:click="removeProduct(product)"
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
                        Update {{ product.product_name }}
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
export default {
  data() {
    return {
      products: null,
    };
  },

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
    // ADD TO CART
    addToCart(index) {
      this.cart.push(index);
    },
    addToCart() {
      fetch("", {
        method: "POST",
        body: JSON.stringify({
          name: "Yellow Butter Cake",
          cost: "",
          image: 1,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((res) => {
          if (res.status == 201) {
            swal({
              text: "Product added in cart",
              icon: "success",
            });
          }
        })
        .catch((err) => console.log("err", err));
    },

    // UPDATE ONE PRODUCTS
    updateProduct() {
      fetch(
        "https://groupapibackend.herokuapp.com/products" + this.product_id,
        {
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
        }
      )
        .then((response) => response.json())
        .then((json) => {
          alert("Product Created");
          this.$router.push({ name: "Products" });
        })
        .catch((err) => {
          alert(err);
        });
    },

    // CREATE PRODUCT
    createProduct() {
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("https://groupapibackend.herokuapp.com/products", {
        method: "POST",
        body: JSON.stringify({
          product_name: this.product_name,
          product_price: this.product_price,
          product_image: this.product_image,
          product_category: this.product_category,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          this.$router.push({ name: "Products" });
        })
        .catch((err) => {
          alert(err);
        });
    },
    // DELETE PRODUCT

    removeProduct: function (index) {
      fetch("https://groupapibackend.herokuapp.com/products/" , {
        method: "DELETE",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
        
      });
console.log(index)
      // this.products.splice(this.index, 1);
    },
    //     deleteEvent: function(event) {
    //   this.events.splice(this.events.indexOf(event), 1);
    // }
  },
};
</script>

<style scoped>
.loading {
  margin-top: 20%;
  justify-content: center;
}
.loading {
  border: 16px solid #f3f3f3;
  position: fixed;
  top: 5%;
  left: 50%;
  border-radius: 50%;
  border-top: 16px solid #000000;
  width: 120px;
  height: 120px;
  -webkit-animation: spin 2s linear infinite; /* Safari */
  animation: spin 2s linear infinite;
}
@-webkit-keyframes spin {
  0% {
    -webkit-transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
.button-body {
  background: rgb(255 212 0);
  border: 0;
  margin-top: 20px;
  color: rgb(0, 0, 0);
  border-radius: 10px;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
  background: #000000;
}

.sub:hover {
  color: rgb(255, 255, 255) !important;
}
.sub {
  color: rgb(0, 0, 0);
}
.sort-content {
  padding: 30px 5px 20px 5px;
}
.sort {
  background-color: white;
  width: 50%;
  border-radius: 15px;
  margin-bottom: 30px;
}
.products {
  padding-top: 50px;
}
.card {
  border-radius: 10px;
}
.subtitlee {
  margin-top: 70px;
}
.card-img-top {
  border-radius: 10px;
}
.containe {
  justify-content: center !important;
}

@media all and (max-width: 991px) {
  .sort {
    width: 60%;
    margin-top: 70px;
  }
}

@media all and (max-width: 768px) {
  .sort {
    width: 70%;
    margin-top: 70px;
  }
  .loading {
    border: 16px solid #f3f3f3;
    position: fixed;
    top: 30%;
    left: 32%;
    border-radius: 50%;
    border-top: 16px solid #000000;
    width: 120px;
    height: 120px;
    -webkit-animation: spin 2s linear infinite; /* Safari */
    animation: spin 2s linear infinite;
  }
}

@media all and (max-width: 576px) {
  .sort {
    width: 80%;
    margin-top: 70px;
  }
}
@media all and (max-width: 400px) {
}
</style>
