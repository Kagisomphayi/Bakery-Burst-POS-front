<template>
<section>
  <div class="home-content">

    <div class="px-4 py-5 my-5 text-center">
    <h1 class="display-5 text-white main-title fw-bold">Bakery Burst</h1>
    <div class="col-lg-6 mx-auto">
      <p class="lead mb-4 text-white">We use only the best ingredients to craft the perfect loaf.</p>
      <div class="d-grid gap-2 d-sm-flex justify-content-sm-center">
        <router-link to="/login">
        <button type="button" class="btn btn-primary btn-warning btn-lg px-4 gap-3">Login</button>
        </router-link>
      </div>
    </div>
  </div>
  </div>

</section>

</template>

<script>


export default {
  name: 'Home',
}
</script>

<style scoped>
    section{
    height: 100vh;
    margin-top: 0;
    background-image: url("../assets/background.jpeg");
    background-repeat: no-repeat;
    background-size: cover !important;
    background-image: linear-gradient(
        0deg,
        rgba(0, 0, 0, 0.5),
        rgba(0, 0, 0, 0.5)
      ),
      url(../assets/background.jpeg);
    overflow-x: hidden;
    overflow-y: hidden;
    background-position: 70%;
  }
  .main-title{
    font-size: 120px;
  }
  .home-content{
margin-top: 15%;
  }
</style>