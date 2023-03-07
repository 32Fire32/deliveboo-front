<script>
import { store } from "../store.js";
import RestaurantCard from "./RestaurantCard.vue";

export default {
  name: "RestaurantsList",
  components: {
    RestaurantCard,
  },
  data() {
    return {
      store,
    };
  },
  created() {
    console.log(store.restaurants);
  },
  
};
</script>

<template>
  <section class="container">
    <div class="row">
      <div class="col-lg-4 my-col" v-for="restaurant in store.restaurants">
       <RestaurantCard :data="restaurant" />
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@media(min-width: 800px) {
  .my-col {
    padding-top: 80px;
  }
}

@media(max-width: 800px) {
  .my-col {
    margin-bottom: 40px;
    padding-right: 40px;
  }
}
</style>
