<script>
import { store } from "../store.js";
import RestaurantCard from "../components/RestaurantCard.vue";

export default {
  name: "restaurant-sponsored",
  components: {
    RestaurantCard,
  },
  data() {
    return {
      store,
    };
  },
  created() {
    console.log('ciaociaociao');
    console.log('ciaociooo')
  },
  computed: {
    filteredRestaurants() {
      const sponsoredRestaurant = store.restaurants.filter(
        (rist) => rist.sponsored
      );
      return sponsoredRestaurant;
    },
  },
};
</script>

<template>
  <section class="container py-5">
    <div class="row">
      <div class="col-lg-4 my-col" v-for="restaurant in filteredRestaurants">
        <RestaurantCard :data="restaurant" />
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>

@media (min-width: 800px) {
  .my-col {
    padding-top: 80px;
  }
}

@media (max-width: 800px) {
  .my-col {
    margin-bottom: 40px;
    padding-right: 40px;
  }
}

</style>
