<template>
  <div id="app">
    <HomePage/>
  </div>
</template>

<script>
  import HomePage from './page/homePage.vue';
export default {
  name: 'App',
  components:{
    HomePage,
  }
}
</script>
<style>
@import url('./style/reset.css');
#app {
  font-family:  'Roboto', sans-serif;
  padding: 20px;
}
</style>
