<template>
  <s-navbar/>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body{
  margin: 0;
  padding: 0;
}

</style>
<script>
import SNavbar from "@/components/navbar/Navbar";
export default {
  components: {SNavbar}
}
</script>
