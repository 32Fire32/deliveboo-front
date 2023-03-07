<template>
  <h1>Categoria: {{ this.$route.params.slug }}</h1>
  <div class="m-4" v-for="restaurant in this.restaurants">
    <div v-for="category in restaurant.categories">
      <div v-if="category.slug == this.$route.params.slug">
        <span>{{ restaurant.name }}</span>
        <router-link
          class="text-decoration-none text-white btn btn-warning rounded-0"
          :to="{ name: 'checkout' }"
          >Menù</router-link
        >
      </div>
    </div>
  </div>

  <div v-for="category in this.restaurants.categories">
    <span>{{ category.name }}</span>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SingleCategory",
  data() {
    return {
      restaurants: null,
      category: [],
    };
  },
  created() {
    axios
      .get(`http://localhost:8000/api/restaurants/`)
      .then((response) => {
        this.restaurants = response.data;
      })
      .catch((err) => {
        console.log(err);
        this.$router.push({ name: "page-404" });
        if (err.response.status === 404) {
        }
      });
  },
};
</script>

<style lang="scss" scoped></style>
