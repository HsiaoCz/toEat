<script setup lang="ts">
import { ref } from 'vue';

/**
 * Restaurants
 * 
 * Name - string
 * Address - string
 * States - string (e.g. "Want to Try" | "Must Try")
 * Dishes - array of Dish objects
 */

interface Restaurant {
  name?: string
  // address?: string
  status?: RestaurantStatus
  dishes?: Dish[]
}

const ALL_STATUS = ["Want to Try", "Recommend", "Must Try"]

type RestaurantStatus = "Want to Try" | "Recommended" | "Do Not Recommend" | "Must try"

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})
const statusList = [
  "Want to Try",
  "Recommended",
  "Do Not Recommend",
  "Must try"
]

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    // address: "",
    status: "Want to Try",
    dishes: []
  })
}
</script>

<template>
  <main>
    <pre>{{ newRestaurant }}</pre>
    <!-- create a form that allows users to add a restourant to a list -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
      </div>
      <!-- <div>
        <label for="restaurant-address">Restaurant Address</label>
        <input id="restaurant-address" v-model="newRestaurant.address" type="text" />
      </div> -->
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <input id="restaurant-status" v-model="newRestaurant.status" type="text" />
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant">
        {{ restaurant }}
      </li>
    </ul>
  </main>
</template>
