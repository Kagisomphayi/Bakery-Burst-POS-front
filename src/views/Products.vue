<template>
  <!-- projects section -->
  <section id="products" class="products">
    <div class="container">
      <div class="pb-5 cont justify-content-center">
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
                @submit.prevent="createProduct"
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
                          v-model="user_name"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="" class="form-label">Category</label>
                        <select
                          class="form-select"
                          name="addCategory"
                          id="addCategory"
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
                          v-model="user_price"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="addImg" class="form-label">Image</label>
                        <input
                          class="form-control"
                          type="text"
                          name="addImg"
                          id="addImg"
                          v-model="image"
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
                        type="submit"
                        class="btn btn-primary"
                        data-bs-dismiss="modal"
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
            v-for="(product, index) in products"
            :key="index"
            class="col-lg-3 col-md-6"
            style="display: flex; justify-content: center"
          >
            <div class="card shadow ani-card" style="width: 18rem">
              <img :src="product.product_image" class="card-img-top" alt="..." />
              <div class="card-body">
                <h4 class="card-title text-black">{{ product.product_name }}</h4>
                <p class="card-text text-black">R{{ product.product.price }}</p>
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
                  v-on:click="removeProduct(index)"
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
                        Update {{ product.name }}
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
                          value="${product.title}"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="editCategory${position}" class="form-label"
                          >Price</label
                        >
                      </div>
                      <div class="mb-3">
                        <label for="editPrice${position}" class="form-label"
                          >Image</label
                        >
                        <input
                          class="form-control"
                          type="text"
                          name="editPrice${position}"
                          id="editPrice${position}"
                          value="${product.price}"
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
                          value="${product.img}"
                        />
                      </div>
                    </div>
                    <div class="modal-footer" >
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
    fetch("https://groupapibackend.herokuapp.com/products/" + this.id, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then(async (json) => {
        this.products = json;
        await fetch(
          "https://groupapibackend.herokuapp.com/users" + json.created_by,
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
            this.products.created_by = json.user_name;
          });
      });
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

    // CREATE PRODUCT
    createProduct() {
      if (!localStorage.getItem("jwt")) {
        alert("User not logged in");
        return this.$router.push({ name: "Login" });
      }
      fetch("", {
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
          alert("Post Created");
          this.$router.push({ name: "Products" });
        })
        .catch((err) => {
          alert(err);
        });
    },
    // DELETE PRODUCT
    removeProduct: function (index) {
      this.items.splice(index, 1);
    },
  },
};
</script>

<style scoped>
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
