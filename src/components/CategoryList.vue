<script>
import { store } from "../store";
import CategoryCard from "./CategoryCard.vue";
import RestaurantsList from "./RestaurantsList.vue";
import RestaurantCard from "./RestaurantCard.vue";
export default {
  name: "CategorysList",
  components: {
    CategoryCard,
    RestaurantCard,
    RestaurantsList,
  },
  data() {
    return {
      store,
      visible: false,
      images: [
        "https://thumbs.dreamstime.com/b/memorial-day-usa-independence-picnic-party-fourth-july-concept-patriotic-american-traditional-food-watermelon-burgers-hot-219579658.jpg",
        "https://shfoodspro.com/wp-content/uploads/2021/02/Vietnamese-Pho.jpg",
        "https://www.limmi.it/wp-content/uploads/2022/05/insalata-ceci-scaled.jpg",
        "https://res.cloudinary.com/hz3gmuqw6/image/upload/c_fill,q_60,w_750/tk-traditional-indian-foods-to-taste-in-2022-phpEXAXNS",
        "https://theplanetd.com/images/Traditional-Italian-Food.jpg",
        "https://cdn4.tuscanynowandmore.com/storage/app/media/discover-italy/bacalao-fish.jpg",
        "https://blog.amigofoods.com/wp-content/uploads/2020/09/mexican-food.jpg",
        "https://www.viaggioff.it/wp-content/uploads/2021/05/poke-bowl-scaled.jpg",
        "https://www.comeindubai.com/wp-content/uploads/2021/04/fast-food-dubai-scaled.jpeg",
        "https://www.thespruceeats.com/thmb/KKVYHEcAN6Jt7yvULfCB4r3ad30=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/what-is-sushi-5079606-hero-01-e5a0a26f194a49478f84e04193baaefa.jpg",
        "https://resize.indiatvnews.com/en/resize/newbucket/715_-/2018/08/tiramisu-1535368950.jpeg",
      ],
    };
  },
  computed: {
    filteredRestaurants() {
      //prendo l'array dei nomi delle categorie
      const selectedCategories = this.store.categories
        .filter((category) => category.selected)
        .map((category) => category.name);
      // filtro i risultati basandomi su quell'array
      return this.store.restaurants.filter((restaurant) => {
        // prendo l'array dei nomi delle categorie per quei ristoranti
        const categoryNames = restaurant.categories.map(
          (category) => category.name
        );
        // controllo se TUTTE le categorie selezionate sono presenti in quelle dei risto
        return selectedCategories.every((category) =>
          categoryNames.includes(category)
        );
      });
    },
    toggleCategory(index) {
      this.store.categories[index].selected =
        !this.store.categories[index].selected;
    },
    isActive() {
      // di base nasconde la sezione dedicata ai ristoranti ma si attiva se almeno uno è selezionato
      return this.store.categories.some((category) => category.selected);
    },
  },
};
</script>
<template>
  <div class="">
    <div class="d-flex flex-column">
      <div class="m-auto">
        <h4 class="mt-5 my-select">Seleziona una o più Categorie</h4>
        <ul
          class="d-flex flex-row flex-wrap w-100 justify-content-start gy-3 col-lg-9 m-auto container-first container category">
          <li v-for="(category, index) in store.categories" :key="index">
            <!-- <div>
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                <input type="checkbox" v-model="category.selected" @change="toggleCategory(index)">
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    {{ category.name }}
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  </div> -->
            <article id="demo" class="feature1">
              <input type="checkbox" id="feature1" v-model="category.selected" @change="toggleCategory(index)" />
              <div class="w-200 d-flex flex-column justify-content-between">
                <img class="img-fluid w-200" :src="images[index]" alt="" />
                <span class="my-span"> {{ category.name }}<br /> </span>
              </div>
            </article>
          </li>
        </ul>
      </div>
      <div class="container">
        <div class="d-flex">
          <ul class="row my-list" v-if="isActive">

            <h4 class="my-title">Hai filtrato: </h4>

            <li class="col-lg-4 my-card" v-for="(restaurant, index) in filteredRestaurants" :key="index">
              <RestaurantCard :data="restaurant" />
              <router-link :to="{
                name: 'single-restaurant',
                params: { slug: restaurant.slug },
              }"></router-link>
            </li>
          </ul>
          <div class="my-container" v-else>
            <h4 class="my-title2">Ristoranti su Deliveboo</h4>
            <RestaurantsList />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.my-list {
  margin-left: -40px;
  margin-top: -50px;
}

.container-first {
  padding: 0px 28px;
}

.my-container {
  margin-top: -50px;
}

.my-category {
  margin-top: -100px;
  margin-bottom: -50px;
}

.my-title {
  margin-bottom: -150px;
  margin-left: 25px;
}

.my-title2 {
  margin-bottom: -180px;
  margin-left: 35px;
}

.my-select {
  margin-bottom: -45px;
  margin-left: 45px;
}

h4 {
  color: rgb(195, 34, 34);
  text-align: start;

}

ul {
  list-style: none;
}

body {
  text-align: center;
  color: #f5f5f5;
  background-image: linear-gradient(-90deg, #0c0c0d, #1a1a1a);
  font-family: "Roboto";
}

.app {
  max-width: 300px;
  margin: 0 auto;
}

article {
  position: relative;
  width: 140px;
  height: 120px;
  margin: 20px;
  float: left;
  border: 2px solid rgb(253, 187, 45);
  box-sizing: border-box;
}

article div {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  line-height: 25px;
  transition: 0.5s ease;
}

article input {
  position: absolute;
  top: 0;
  left: 0;
  width: 140px;
  height: 100px;
  opacity: 0;
  cursor: pointer;
}

#demo {
  -webkit-box-shadow: 0px 0px 25px 0px #ffc44a;
  box-shadow: 0px 0px 25px 0px #ffc44a;
}

#demo:hover {
  transform: scale(1.2);
  /* (150% zoom - Note: if the zoom is too large, it will go outside of the viewport) */
}

input[type="checkbox"]:checked~div {
  background-color: rgb(253, 187, 45);
}

.category {
  color: rgb(195, 34, 34);
  font-size: 18px;
}

.container {
  margin-top: 50px;
  padding-top: 50px;
}

.my-card {
  margin-top: 25px;
  margin-bottom: 25px;
}
</style>
