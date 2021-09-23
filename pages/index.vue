<template >
<div class="mybackground">
  <div class="container">

  <Home />


  </div>
  </div>
</template>

<script>
import Home from '../components/Home.vue'
  export default {
    components: { Home,}
  }
</script>

<style  scoped>
.mybackground {
  background: rgb(219, 241, 247);
  	height: auto! important;
	min-height: 100vh;
   
	font-family: 'Montserrat', sans-serif;
}

</style>