<script setup lang="ts">
import { ref } from 'vue'
import type { RestaurantStatus, Diet } from '@/types';
interface Dish{
  name?: string,
  diet?: Diet,
  status?: RestaurantStatus
}


const statusList = ['Do not Recommend', 'Recommend', 'Want to Try', 'Must Try']
const dishList = ref<Dish[]>([])
const newDish = ref<Dish>({})
function addDish() {
  dishList.value.push({
    name: newDish.value.name,
    status: newDish.value.status,
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newDish }}
    </pre>
    <form @submit.prevent="addDish">
      <div>
        <label for="dish-name">Dish Name</label>
        <input id="dish-name" v-model="newDish.name" type="text" />
      </div>
      <div>
        <label for="dish-status">Dish Status</label>
        <select name="dish-status" id="dish-status" v-model="newDish.status">
          <option v-for="status in statusList" :key="status" :value="status">{{ status }}</option>
        </select>
      </div>

      <button type="submit">Add Dish</button>
    </form>
    <ul>
      <li v-for="dish in dishList" :key="dish.name">
        {{ dish.name }} - {{ dish.status }} 
      </li>
    </ul>
  </main>
</template>
