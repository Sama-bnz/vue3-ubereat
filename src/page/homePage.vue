<template>
  <div class="homePage">
    <div class="header">
      <img src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg" alt="logo_uber">
      <div class="wrapper--input">
        <input v-model="user_search_restaurant" type="text" placeholder="De quoi avez-vous envie?">
        <div class="search">
          <router-link to="/restaurantPage">
            <div v-for="(restaurant, i) in search_restaurant" :key="i" class="container--restaurant--search">
            <div class="wrapper--img">
              <img :src="restaurant.image" alt="">
            </div>
              <p>{{restaurant.name}}</p>
            </div>
          </router-link>
        </div>
      </div>
    </div>
    <div class="banniere">

    </div>
    <RestaurantRow v-for="(data, i) in data_restaurant" :key="i" :current_restaurant="data"/>
  </div>
</template>

<script>
//IMPORT BDD
import bdd from '../bdd.js'
import { onMounted, ref, watch } from 'vue';
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
      let all_restaurant = [];

      const makeDataRestaurant = () => {
        let current_restaurant = [];

        for (const restaurant of bdd) {
          const new_restaurant = new Restaurant(restaurant.name, restaurant.note,restaurant.image, restaurant.drive_time)
          //make all restaurant array 
          all_restaurant.push(new_restaurant);

          if(current_restaurant.length === 2) {
            current_restaurant.push(new_restaurant)
            data_restaurant.value.push(current_restaurant)
            current_restaurant = [];
          } else {
            current_restaurant.push(new_restaurant);
          }
        }
      }

      //User search restaurant
      let user_search_restaurant = ref('');

      let search_restaurant = ref([]);

      watch(user_search_restaurant, new_value => {

        let regex = RegExp(new_value.toLowerCase());

        let new_search_restaurant =  all_restaurant.filter( restaurant => regex.test(restaurant.name.toLowerCase()));

        search_restaurant.value = new_search_restaurant;

        new_value == 0 ? search_restaurant.value = [] : search_restaurant.value = new_search_restaurant
      })
      //
      onMounted(makeDataRestaurant);

      return {
        data_restaurant,
        user_search_restaurant,
        search_restaurant
      }
    },
}
</script>

<style lang="scss">
  .homePage {
    .header{
      height: 100px;
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      img{
        width: 200px;
      }

      .wrapper--input {
        position: relative;

        input {
        background-color: #f6f6f6;
        border: none;
        height: 70px;
        width: 400px;
        outline: none;
        padding-left: 20px;
        }
        .search {
          position: absolute;
          top: 100%;
          width: 100%;
          background-color: #fff;

          .container--restaurant--search {
            display: flex;
            align-items: center;
            padding: 10px;

            &:hover {
              background: #f6f6f6;
            }
            
            .wrapper--img {
              height: 60px;
              width: 60px;
              margin-right: 25px;
              border-radius: 50%;
              overflow: hidden;

              img {
                height: 100%;
                width: auto;
              }
            }
          }
        }
      }
      
    }
    .banniere {
      height: 200px;
      width: 100%;
      background-image: url('../assets/uber-eats-image-uber.jpg');
      background-size: cover;
      background-position: center center;
    }
  }
</style>