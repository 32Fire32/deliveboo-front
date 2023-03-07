<template>
  <div v-if="restaurant" class="text-center my-restaurant">
    <div class="container">
      <div class="row">
        <div class="col-lg-6 info">
          <h1 class="name">{{ restaurant.name }}</h1>
          <img
            class="my-img"
            v-if="restaurant.img"
            :src="restaurant.img"
            :alt="restaurant.name"
          />
          <div class="text-center">
            <div class="m-2">{{ restaurant.description }}</div>
            <div class="m-2">{{ restaurant.address }}</div>
            <div class="m-2">Orario Apertura {{ restaurant.opening_time }}</div>
            <div class="m-2">Orario Chiusura {{ restaurant.closing_time }}</div>
            <span class="m-2"
              >Costo spedizione: {{ restaurant.price_shipping }}€</span
            >
          </div>
        </div>
        <div class="col-lg-6 dish">
          <!-- form -->
          <form @submit.prevent="saveData()">
            <h5>I NOSTRI PIATTI:</h5>

            <div class="d-flex flex-wrap">
              <!-- <button @click="showlog">Log</button> -->
              <div v-for="(dish, index) in restaurant.dishes" :key="index">
                <article class="wrapper" id="demo">
                  <input
                    :id="'check-' + index"
                    class="check ms-1 mt-2 selected"
                    type="checkbox"
                    :value="dish"
                    @click="this.selectDish(index)"
                    v-model="order.dish"
                  />
                  <div
                    :style="`background-image: url(${dish.img});background-color: black; background-size:cover; background-position:center; background-repeat: no-repeat;  background-color: white;`"
                  >

                  </div>
                </article>
                <div class="d-flex flex-column">
                  <label :for="'check-' + index">{{ dish.name }}</label>
                  <label :for="'check-' + index">{{ dish.price }}€</label>
                </div>
              </div>
            </div>

            <div class="addcart">
              <button class="text-white btn rounded-3 m-4" type="submit">
                Aggiungi al carrello
              </button>
            </div>

            <!-- tasto carrello -->

            <!-- modale -->
            <div
              id="myModal"
              class="modal fade"
              role="dialog"
              style="display: none"
            >
              <form @submit.prevent="overWriteCart()">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h4 class="modal-title">ATTENZIONE</h4>
                    </div>
                    <div class="modal-body">
                      <p>ATTENZIONE STAI MODIFICANDO IL CARRELLO!</p>
                    </div>
                    <div class="modal-footer d-flex justify-content-center">
                      <button
                        id="cart"
                        class="text-white btn rounded-3 m-4"
                        type="submit"
                      >
                        Aggiungi al Carrello
                      </button>
                      <button
                        type="button"
                        class="btn btn-secondary"
                        data-bs-dismiss="modal"
                      >
                        Close
                      </button>
                      <p id="confirmed" class="d-none">CARRELLO MODIFICATO!</p>
                    </div>
                  </div>
                </div>
              </form>
            </div>
            <!-- modale -->

            <div id="advise" class="d-none">
              <p>Non puoi ordinare da più ristoranti contemporaneamente!</p>
            </div>
            <div id="success" class="d-none">
              <p>Piatti aggiunti al carrello!</p>
            </div>
            <div id="warning" class="d-none">
              <p>Piatto già presente nel carrello!</p>
            </div>
            <div id="select" class="d-none">
              <p>Seleziona almeno un piatto!</p>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { store } from "../store";
import axios from "axios";
export default {
  name: "SingleRestaurant",
  data() {
    return {
      components: {
        store,
      },
      restaurant: null,
      order: {
        dish: [],
      },
    };
  },
  methods: {
    selectDish(index) {
      document
        .querySelector(`#check-${index}`)
        .parentElement.classList.toggle("selected");
    },
    overWriteCart() {
      localStorage.removeItem("my_data");

      localStorage.setItem("my_data", JSON.stringify(this.order));
      localStorage.setItem("slug", JSON.stringify(this.$route.params.slug));
      localStorage.setItem("price_shipping", JSON.stringify(this.restaurant));

      store.userCart = JSON.parse(localStorage.getItem("my_data"));

      document.getElementById("confirmed").classList.remove("d-none");
      setTimeout(function () {
        document.getElementById("confirmed").classList.add("d-none");
      }, 5000);

      document.getElementById("cart").classList.add("d-none");
    },

    saveData() {
      if (store.userCart) {
        document.getElementById("cart").classList.remove("d-none");

        if (this.order.dish.length != 0) {
          let foundMatchingRestaurant = false;
          store.userCart.dish.forEach((element) => {
            if (element.restaurant_id === this.restaurant.id) {
              foundMatchingRestaurant = true;
            }
          });

          if (store.userCart.dish.length > 0 && !foundMatchingRestaurant) {
            document.getElementById("advise").classList.remove("d-none");

            setTimeout(function () {
              document.getElementById("advise").classList.add("d-none");
            }, 5000);
          } else {
            if (store.userCart.dish.length > 0 && foundMatchingRestaurant) {
              store.userCart.dish.forEach((cartDish) => {
                this.order.dish.forEach((menuDish) => {
                  if (cartDish.name === menuDish.name) {
                    document
                      .getElementById("warning")
                      .classList.remove("d-none");

                    setTimeout(function () {
                      document
                        .getElementById("warning")
                        .classList.add("d-none");
                    }, 5000);
                  } else {
                    $("#myModal").modal("show");
                  }
                });
              });
            } else {
              localStorage.setItem("my_data", JSON.stringify(this.order));
              localStorage.setItem(
                "slug",
                JSON.stringify(this.$route.params.slug)
              );
              localStorage.setItem(
                "price_shipping",
                JSON.stringify(this.restaurant)
              );

              store.userCart = JSON.parse(localStorage.getItem("my_data"));

              document.getElementById("success").classList.remove("d-none");

              setTimeout(function () {
                document.getElementById("success").classList.add("d-none");
              }, 5000);
            }
          }
        } else {
          document.getElementById("select").classList.remove("d-none");
        }
      } else {
        localStorage.setItem("my_data", JSON.stringify(this.order));
        localStorage.setItem("slug", JSON.stringify(this.$route.params.slug));
        localStorage.setItem("price_shipping", JSON.stringify(this.restaurant));

        store.userCart = JSON.parse(localStorage.getItem("my_data"));

        document.getElementById("success").classList.remove("d-none");

        setTimeout(function () {
          document.getElementById("success").classList.add("d-none");
        }, 5000);
      }
    },

    showlog() {
      // console.log(store.userCart.dish)
      console.log(localStorage.getItem("my_data"));
      console.log(this.order.dish.length);
      console.log(store.userCart.dish.length);
    },

    disableInput() {
      for (let i = 0; i < this.restaurant.dishes.length; i++) {
        if (document.querySelector(`.check_${i}`).checked === true) {
          document.querySelector(`.input_${i}`).disabled = false;
        } else if (document.querySelector(`.check_${i}`).checked === false) {
          document.querySelector(`.input_${i}`).value = "";
          document.querySelector(`.input_${i}`).disabled = true;
        }
      }
    },
  },
  created() {
    axios
      .get(`http://localhost:8000/api/restaurants/${this.$route.params.slug}`)
      .then((response) => {
        this.restaurant = response.data;
        // console.log(this.restaurant)
      })
      .catch((err) => {
        console.log(err);
        this.$router.push({ name: "page-404" });
        // if (err.response.status === 404) {
        // }
      });

    store.userCart = JSON.parse(localStorage.getItem("my_data"));

    this.restaurant_slug = JSON.parse(localStorage.getItem("slug"));
    this.rest = JSON.parse(localStorage.getItem("price_shipping"));
  },
};
</script>

<style lang="scss" scoped>
.selected {
  filter: grayscale(100%) brightness(35%) sepia(100%) hue-rotate(-50deg)
    saturate(700%) contrast(0.8) !important;
}
.dish-text {
  color: black;
}
.my-restaurant {
  background-color: rgb(253, 187, 45);
}

.name {
  padding-top: 10px;
  color: rgb(195, 34, 34);
  font-size: 60px;
  font-weight: 700;
}

h5 {
  color: rgb(195, 34, 34);
  font-weight: 700;
  font-size: 30px;
}

.btn {
  background-color: rgb(195, 34, 34);
}

.info {
  color: white;
  font-size: 20px;
  font-weight: 700;
}

.dish {
  border-radius: 15px;
  padding-top: 60px;
}

.quant {
  width: 50px;
}

.my-img {
  padding-top: 30px;
  padding-bottom: 30px;
  width: 400px;
}

article {
  border-radius: 5px;
  overflow: hidden;
  position: relative;
  width: 110px;
  height: 80px;
  margin: 20px;
  // float: left;
  border: 2px solid rgb(195, 34, 34);
  box-sizing: border-box;
  background-color: black !important;
  color: rgb(253, 187, 45);
  font-weight: 700;
  font-size: 17px;
  text-align: center;
  transition: all 0.1s;
}

article div {
  width: 100%;
  height: 100%;
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
  -webkit-box-shadow: 0px 0px 25px 0px rgb(195, 34, 34);
  box-shadow: 0px 0px 25px 0px rgb(195, 34, 34);
}

#demo:hover {
  transform: scale(1.2);
  /* (150% zoom - Note: if the zoom is too large, it will go outside of the viewport) */
}

input[type="checkbox"]:checked ~ div {
  background-color: rgb(195, 34, 34);
}

#advise,
#warning,
#select {
  color: rgb(195, 34, 34);
  font-size: 20px;
  font-weight: 700;
}

#success {
  color: green;
  font-size: 20px;
  font-weight: 700;
}

@media (max-width: 798px) {
  .dish {
    margin-top: 10px;
  }

  .info {
    margin-bottom: 10px;
    margin-top: 100px;
    padding-bottom: 30px;
  }
}

@media (min-width: 800px) and (max-width: 991px) {
  .info {
    margin-top: 50px;
    margin-bottom: 10px;
    margin-top: 150px;
  }
}

@media (min-width: 768px) and (max-width: 991px) {
  article {
    right: -8%;
  }
}

@media (min-width: 992px) and (max-width: 1399px) {
  .dish {
    margin-top: 120px;
  }
  .info {
    margin-bottom: 50px;
    padding-bottom: 30px;
    margin-top: 150px;
  }
  article {
    right: -10%;
  }
}

@media (min-width: 1400px) {
  .dish {
    margin-top: 150px;
  }

  .info {
    margin-bottom: 50px;
    margin-top: 180px;
    padding-bottom: 30px;
  }
  article {
    right: -4%;
  }
}
</style>
