<script setup lang="ts">
import { ref } from 'vue'
import type { RestaurantStatus, Diet } from '@/types';
interface Restaurant {
  name?: string
  address?: string
  status?: RestaurantStatus
  dishes?: Dish[]
}

interface Dish{
  name: string,
  diet?: Diet,
  status?: RestaurantStatus
}
// enum RestaurantStatus{
//   Recommended = 'Recommended',
//   WantToTry = 'Want to Try',
//   MustTry = 'Must Try'
// }


const statusList = ['Do not Recommend', 'Recommend', 'Want to Try', 'Must Try']
const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})
function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    address: newRestaurant.value.address,
    status: newRestaurant.value.status,
    dishes: []
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newRestaurant }}
    </pre>
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
      </div>
      <div>
        <label for="restaurant-address">Restaurant Address</label>
        <input id="restaurant-address" v-model="newRestaurant.address" type="text" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <select name="restaurant-status" id="restaurant-statis" v-model="newRestaurant.status">
          <option v-for="status in statusList" :key="status" :value="status">{{ status }}</option>
        </select>
      </div>

      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant.name }} - {{ restaurant.status }} at {{ restaurant.address }}
      </li>
    </ul>
  </main>
</template>
