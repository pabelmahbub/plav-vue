<template>
  <NavbarTop />
  <HomeView  style="margin-top:100px"/>
  <router-view />
</template>

<script>
import NavbarTop from './components/NavbarTop.vue';

export default {
  name: 'App',
  components: {
    NavbarTop,
  }
}
</script>

<style>
body{
  
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #555;
  max-width: 800px;
  margin: 0 auto;
}
</style>
