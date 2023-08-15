<template>
  <div class="homePage">
    <RestaurantRow v-for="(data, i) in data_restaurant" :key="i" :current_restaurant="data"/>
  </div>
</template>

<script>
//IMPORT BDD
import bdd from '../bdd.js'
import { onMounted, ref } from 'vue';
//IMPORT COMPONENT
import RestaurantRow from '../components/RestaurantRow.vue'
export default {
    name: 'HomePage',
    components: {
      RestaurantRow
    },
    setup() {
      class Restaurant {
        constructor (name, note, image, drive_time) {
          this.name = name;
          this.note = note;
          this.image = image;
          this.drive_time = drive_time;
        }
      }

      let data_restaurant = ref([]);

      const makeDataRestaurant = () => {
        let current_restaurant = [];

        for (const restaurant of bdd) {
          const new_restaurant = new Restaurant(restaurant.name, restaurant.note,restaurant.image, restaurant.drive_time)

          if(current_restaurant.length === 2) {
            current_restaurant.push(new_restaurant)
            data_restaurant.value.push(current_restaurant)
            current_restaurant = [];
          } else {
            current_restaurant.push(new_restaurant);
          }
        }
      }
      onMounted(makeDataRestaurant);

      return {
        data_restaurant,
      }
    },
}
</script>

<style>

</style>