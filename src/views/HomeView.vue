<script setup lang="ts">
import { ref } from 'vue'

interface Restaurant {
  name?: string
  status?: enumStatus
  dishes?: Dish[]
}

type Dish = string
const ALL_STATUS = ["Want to try", "Must try", "Avoid"]

type enumStatus = "Want to try" | "Must try" | "Avoid"


const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})
function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    status: 'Want to try',
    dishes: newRestaurant.value.dishes
  })
}
</script>

<template>
  <main>
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name:</label> &nbsp;
        <input type="text" id="restaurant-name" v-model="newRestaurant.name">
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status:</label> &nbsp;
        <select id="restaurant-status" v-model="newRestaurant.status">
          <option v-for="status in ALL_STATUS" :key="status" :value="status">
            {{ status }}
          </option>
        </select>
      </div>
      <div>
        <label for="restaurant-dishes">Restaurant Dishes:</label> &nbsp;
        <input type="text" id="restaurant-dishes" v-model="newRestaurant.dishes">
      </div>

      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant }}
      </li>
    </ul>
  </main>
</template>
