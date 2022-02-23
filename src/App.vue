<template>
<Navbar/>
  <router-view/>

</template>

<script>
import Navbar from './components/Navbar'
export default {
  components:{
    Navbar
  }

};
</script>

<style>
body{
  background-color: rgb(255 212 0);
}


</style>
