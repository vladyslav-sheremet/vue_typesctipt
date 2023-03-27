<script setup lang="ts">
import { ref } from 'vue'
import type {RecommendStatus, Dish} from '@/types'
import {restaurantStatusList} from '@/constant'

interface Restaurant {
  name?: string
  status?: RecommendStatus
  dishes?: Dish[]
}

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({
  status: 'Want to Try'
})

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    status: newRestaurant.value.status,
    dishes: []
  })
}
</script>

<template>
  <main>
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant name</label>
        <input id="restaurant-name" type="text" v-model="newRestaurant.name" />
      </div>

      <div>
        <label for="restaurant-status">Restaurant status</label>
        <select name="restaurant-status" id="restaurant-status" v-model="newRestaurant.status">
          <option v-for="status in restaurantStatusList" :key="status" :value="status">
            {{ status }}
          </option>
        </select>
      </div>

      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant.name }}
        {{ restaurant.status }}
      </li>
    </ul>
  </main>
</template>
