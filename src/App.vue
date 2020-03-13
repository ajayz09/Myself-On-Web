<template>
  <div id="app">
    <Landing />
  </div>
</template>

<script>

import Landing from './components/Landing.vue'
export default {
  name: 'app',
  components: {
    Landing
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  /* margin-top: 60px; */

}
html {
    overflow: hidden;
    height: 100%;
  }
  body {
    background-color: rgb(44,62,80);
    height: 100%;
    overflow: auto;
    margin: 0;
  }
</style>
