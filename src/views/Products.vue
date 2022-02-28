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
                          v-model="name"
                        />
                      </div>
                      <div class="mb-3">
                        <label for="addPrice" class="form-label">Price</label>
                        <input
                          class="form-control"
                          type="text"
                          name="addPrice"
                          id="addPrice"
                          v-model="price"
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
              <img :src="product.image" class="card-img-top" alt="..." />
              <div class="card-body">
                <h4 class="card-title text-black">{{ product.name }}</h4>
                <p class="card-text text-black">R{{ product.cost }}</p>
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
                  data-bs-target="#editProduct${position}"
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
      name: "",
      price: "",
      image: "",
      cart: [],
      products: [
        {
          name: "Cake",
          cost: "0.99",
          image:
            "https://images.unsplash.com/photo-1578985545062-69928b1d9587?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1089&q=80",
        },
        {
          name: "Cake",
          cost: "5.99",
          image:
            "https://images.unsplash.com/photo-1588195538326-c5b1e9f80a1b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MTh8fGNha2VzfGVufDB8fDB8fA%3D%3D&auto=format&fit=crop&w=500&q=60",
        },
        {
          name: "Cookies",
          cost: "0.99",
          image:
            "https://images.unsplash.com/photo-1597733153203-a54d0fbc47de?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1090&q=80",
        },
        {
          name: "Cake",
          cost: "5.99",
          image:
            "https://images.unsplash.com/photo-1588195538326-c5b1e9f80a1b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1050&q=80",
        },
        {
          name: "Cup cakes",
          cost: "$0.99",
          image:
            "https://images.unsplash.com/photo-1550617931-e17a7b70dce2?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80",
        },
      ],
    };
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
          name: this.name,
          price: this.price,
          image: this.image,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
      })
        .then((response) => response.json())
        .then((json) => {
          alert("Post Created");
          this.$router.push({ name: "Blogs" });
        })
        .catch((err) => {
          alert(err);
        });
    },
  // DELETE PRODUCT
    removeProduct: function (index) {
    this.items.splice(index, 1);
  }

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
