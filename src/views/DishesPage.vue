<script setup lang="ts">
import { ref } from 'vue'
import type {Dish} from '@/types'
import {restaurantStatusList} from '@/constant'

const dishList = ref<Dish[]>([])
const newDish = ref<Dish>({
  status: 'Want to Try'
})

function addDish() {
  dishList.value.push({
    name: newDish.value.name,
    status: newDish.value.status
  })
}
</script>

<template>
  <main>
    <form @submit.prevent="addDish">
      <div>
        <label for="dish-name">Dish name</label>
        <input id="dish-name" type="text" v-model="newDish.name" />
      </div>

      <div>
        <label for="dish-status">Dish status</label>
        <select name="dish-status" id="dish-status" v-model="newDish.status">
          <option v-for="status in restaurantStatusList" :key="status" :value="status">
            {{ status }}
          </option>
        </select>
      </div>

      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="dish in dishList" :key="dish.name">
        {{ dish.name }}
        {{ dish.status }}
      </li>
    </ul>
  </main>
</template>
