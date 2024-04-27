<template>

<MainPage />

  
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

import MainPage from './components/MainPage.vue'


export default {
  name: 'App',
  // components: {
  //   HelloWorld
  // }
  components: {
   MainPage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
