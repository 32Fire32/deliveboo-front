<script>
import { store } from "../store";
import RestaurantsList from "../components/RestaurantsList.vue";
export default {
  name: "Restaurants",
  components: {
    RestaurantsList,
  },
  data() {
    return {
      store,
    };
  },
};

</script>

<template>
  <div class="container">
    <h2>Ristoranti 2</h2>
    <RestaurantsList class="my-restaurant" />
  </div>
  <div class="mt-5">
    <CategoryList class="text-center" />
  </div>
</template>

<style lang="scss" scoped>
.my-restaurant {
  margin: 70px 0 80px;
}
</style>
