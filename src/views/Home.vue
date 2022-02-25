<template>
<section><h1>hello</h1></section>

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
        rgba(0, 0, 0, 0.2),
        rgba(0, 0, 0, 0.2)
      ),
      url(../assets/background.jpeg);
    overflow-x: hidden;
    overflow-y: hidden;
    background-position: 70%;
  }
</style>