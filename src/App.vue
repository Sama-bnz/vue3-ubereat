<template>
  <div id="app">
    <RestaurantCard/>
  </div>
</template>

<script>
import RestaurantCard from './components/RestaurantCard.vue';
export default {
  components: { RestaurantCard },
  name: 'App',
  component:{
    RestaurantCard
  }
}
</script>
<style>
@import url('./style/reset.css');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wgth@300:400:700&display=swap');
#app {
  font-family:  'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
