<template>
  <h2 class="subtitlee" style="text-align: center">User Profile Card</h2>

  <div class="card" v-for="(user, index) in users" :key="index">
    <h1>{{ user.user_name }}</h1>
    <p class="title">{{ user.user_email }}</p>
    <p>{{ user.user_contactNumber }}</p>
    <p>{{ user.join_Date }}</p>
    <button
      type="button"
      class="btn border-dark mx-2 card-btn"
      v-on:click="deleteUser(index)"
    >
      <i class="bi bi-trash3"></i>
    </button>
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
    fetch("https://groupapibackend.herokuapp.com/users/" , {
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
};
</script>

<style>
.subtitlee {
  margin-top: 100px;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 600px;
  height: 300px;
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
</style>
