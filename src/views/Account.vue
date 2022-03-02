<template>

<div class="container">
<div v-if="users">
   <h2 class="subtitlee" style="text-align: center">Users</h2>

<div class="row col-lg-12 proji" style="row-gap: 10px; column-gap:1px">
  <div class="card pt-5 col-lg-3 col-md-6" v-for="(user, _id) in users" :key="_id">
    <h1>{{ user.user_name }}</h1>
    <p class="title">{{ user.user_email }}</p>
    <p>{{ user.user_contactNumber }}</p>
    <p>{{ user._id }}</p>
    <p>{{ user.join_Date }}</p>
    <button
      type="button"
      class="btn mx-2 card-btn"
      v-on:click="deleteUser(_id)"
    >
      <i class="bi bi-trash3"></i>
    </button>
  </div> 
  </div>
</div>
<div class="loading" v-else></div>

</div>

</template>

<script>
export default {

  data() {
    return {
      users: null,
    };
  },
    mounted() {
    fetch("https://groupapibackend.herokuapp.com/users/", {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8",
        Authorization: `Bearer ${localStorage.getItem("jwt")}`,
      },
    })
      .then((response) => response.json())
      .then(async (json) => {
        this.users = json;
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
            this.users.created_by = json.user_name;
          });
      });
  },
  methods:{
        deleteUser: function (_id) {
      fetch("https://groupapibackend.herokuapp.com/users/" + _id , {
        method: "DELETE",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
          Authorization: `Bearer ${localStorage.getItem("jwt")}`,
        },
        
      });
        console.log(_id)
      // this.products.splice(this.index, 1);
    },
  }
};
</script>

<style>
.loading {
  margin-top: 20%;
  justify-content: center;
}
.loading {
  border: 16px solid #f3f3f3;
  position: fixed;
  top: 20%;
  left: 50%;
  border-radius: 50%;
  border-top: 16px solid #000000;
  width: 120px;
  height: 120px;
  -webkit-animation: spin 2s linear infinite; /* Safari */
  animation: spin 2s linear infinite;
}
@-webkit-keyframes spin {
  0% { -webkit-transform: rotate(0deg); }
  100% { -webkit-transform: rotate(360deg); }
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
.subtitlee {
  margin-top: 100px;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 200px;
  height: 250px;
  margin: auto;
  margin-top: 50px;
  text-align: center;
  font-family: arial;
}

.title {
  color: grey;
  font-size: 18px;
}

button {
  border: none;
  outline: 0;
  display: inline-block;
  padding: 8px;
  color: white;
  background-color: #000;
  text-align: center;
  cursor: pointer;
  width: 100%;
  font-size: 18px;
}

a {
  text-decoration: none;
  font-size: 22px;
  color: black;
}

button:hover,
a:hover {
  opacity: 0.7;
}
@media all and (max-width: 700px) {
  .loading {
  border: 16px solid #f3f3f3;
  position: fixed;
  top: 15%;
  left: 32%;
  border-radius: 50%;
  border-top: 16px solid #000000;
  width: 120px;
  height: 120px;
  -webkit-animation: spin 2s linear infinite; /* Safari */
  animation: spin 2s linear infinite;
}
}
</style>
