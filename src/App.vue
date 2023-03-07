<script>
import { store } from "./store";
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppFooter from "./components/AppFooter.vue";

export default {
  components: {
    AppHeader,
    AppMain,
    AppFooter,
  },
  data() {
    return {
      store,
    };
  },
  created() {
    axios.get("http://127.0.0.1:8000/api/restaurants").then((response) => {
      store.restaurants = response.data;
      // console.log(response.data)
    });
    axios.get("http://127.0.0.1:8000/api/categories").then((response) => {
      store.categories = response.data;
      // console.log(this.store.categories)

    });
  },
};
</script>

<template>
  <div>
    <AppHeader class="my-header" />
    <AppMain class="my-main" />
    <AppFooter class="my-footer" />
  </div>
</template>

<style lang="scss">
@import "./style/global.scss";

body {
  font-family: 'Lato', sans-serif;
}

.my-header {
  height: 80px;
}

.my-main {
  flex-grow: 1;



}
</style>
