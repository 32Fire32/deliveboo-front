<script>
import { store } from "../store";
import axios from "axios";
export default {
  name: "Cart",
  data() {
    return {
      store,
      rest: null,
      restaurant_slug: null,
      restaurant: null,
      totalPrice: [],
      subtotal: 0,
      orderData: {
        firstname: "",
        lastname: "",
        code: null,
        price: 0,
        address: "",
        email: "",
        phone_number: "",
        order_date: null,
        additional_info: "",
      },
      cartItems: {
        dishesId: [],
        dishesQuantity: [],
      },
      orderError: false,
      shipping: "",
    };
  },
  methods: {
    addNewOrder() {
      axios
        .post(`http://localhost:8000/api/orders/${this.restaurant_slug}`, {
          firstname: this.orderData.firstname,
          lastname: this.orderData.lastname,
          code: this.orderData.code,
          price: this.orderData.price,
          address: this.orderData.address,
          email: this.orderData.email,
          phone_number: this.orderData.phone_number,
          order_date: this.orderData.order_date,
          additional_info: this.orderData.additional_info,
          dishes_Id: this.cartItems.dishesId,
          tot_quantity: this.cartItems.dishesQuantity,
        })
        .then((response) => {
          store.userCart = [];
          console.log(store.userCart);
          localStorage.clear();
        })
        .catch((err) => { });
        document.querySelector('.btn-close').click();
        this.$router.push("/ordine");
    },
    showlog() {
      for (let i = 0; i < store.userCart.dish.length; i++) {
        this.cartItems.dishesQuantity.push(
          parseFloat(document.querySelector(`#quantity-${i}`).value)
        );
      }
      console.log(this.cartItems.dishesQuantity);
    },
    // addZeroToNumber(num) {
    //     if (num != undefined) {
    //         if (num.toString().includes(".")) {
    //             return num+"0"
    //         } else return num+".00"
    //     }
    // },
    pushPriceInArray(item) {
      this.orderTotal.push(item);
    },
    // orderTotalPrice() {
    //     if (this.orderTotal.length != 0)
    //     return this.orderTotal.reduce(function(a, b){
    //         return a + b;
    //     })
    // },
    QuantityUp(i, price) {
      let oldPrice = price;
      // CALCOLO QUANTITA' / PREZZO
      document.querySelector(`#quantity-${i}`).stepUp();
      document.querySelector(`#price-${i}`).innerHTML =
        price * document.querySelector(`#quantity-${i}`).value;
      if (document.querySelector(`#quantity-${i}`).value == 10) {
        document.querySelector(`#up-btn-${i}`).disabled = true;
      }
      if (document.querySelector(`#down-btn-${i}`).disabled == true) {
        document.querySelector(`#down-btn-${i}`).disabled = false;
      }
      if (document.querySelector(`#quantity-${i}`).value <= 10) {
        this.totalPrice[i] += parseFloat(oldPrice);
        this.subtotal = this.totalPrice.reduce((pv, cv) => pv + cv, 0);
        this.orderData.price = this.shipping + this.subtotal;
      }

      // AGGIUNGI ZERO ALLA FINE
      if (document.querySelector(`#price-${i}`).innerHTML.includes(".")) {
        document.querySelector(`#price-${i}`).innerHTML += "0";
      } else document.querySelector(`#price-${i}`).innerHTML += ".00";
    },
    QuantityDown(i, price) {
      let oldPrice = price;
      // CALCOLO QUANTITA' / PREZZO
      if (document.querySelector(`#up-btn-${i}`).disabled == true) {
        document.querySelector(`#up-btn-${i}`).disabled = false;
      }
      if (document.querySelector(`#quantity-${i}`).value < 3) {
        document.querySelector(`#down-btn-${i}`).disabled = true;
      }
      if (parseFloat(document.querySelector(`#price-${i}`).innerHTML) > price) {
        document.querySelector(`#quantity-${i}`).stepDown();
        document.querySelector(`#price-${i}`).innerHTML -= price;
      } else {
        document.querySelector(`#price-${i}`).innerHTML = price;
      }
      if (this.totalPrice[i] > oldPrice) {
        this.totalPrice[i] -= parseFloat(oldPrice);
        this.subtotal = this.totalPrice.reduce((pv, cv) => pv + cv, 0);
        this.orderData.price = this.shipping + this.subtotal;
        // console.log(this.orderData.price)
      }

      if (document.querySelector(`#price-${i}`).innerHTML.includes(".")) {
        document.querySelector(`#price-${i}`).innerHTML += "0";
      } else document.querySelector(`#price-${i}`).innerHTML += ".00";
    },

    getQuantities() {
      console.log(this.cartItems.dishesQuantity);
      if (this.cartItems.dishesQuantity.length > 0) {
        this.cartItems.dishesQuantity = [];
      } else {
        store.userCart.dish.forEach((element, i) => {
          this.cartItems.dishesQuantity.push(
            parseFloat(document.querySelector(`#quantity-${i}`).value)
          );
        });
        console.log(this.cartItems.dishesQuantity);
      }
    },
    clearQuantities() {
      this.cartItems.dishesQuantity = [];
    },
    addZeroToPrice() {

    },
    deleteCart(i) {
      store.userCart.dish.splice(i, 1);

      localStorage.removeItem('my_data')

      localStorage.setItem('my_data', JSON.stringify(store.userCart));


      if (store.userCart.dish.length === 0) {
        localStorage.clear();

      }
      this.$router.go(0);
    },
  },
  // computed: {
  //     getQuantities() {
  //                 for (let i = 0; i < store.userCart.dish.length; i++) {

  //                     this.cartItems.dishesQuantity.push(parseFloat(document.querySelector(`#quantity-${i}`).value))
  //                 console.log(this.cartItems.dishesQuantity)

  //                 }
  //     },
  // },
  created() {
    store.userCart = JSON.parse(localStorage.getItem("my_data"));

    this.restaurant_slug = JSON.parse(localStorage.getItem("slug"));
    this.rest = JSON.parse(localStorage.getItem("price_shipping"));
  },
  mounted() {
    if(store.userCart){
      document.getElementById('card-number').addEventListener('input', function (e) {
      e.target.value = e.target.value.replace(/[^\dA-Z]/g, '').replace(/(.{4})/g, '$1 ').trim();
    });

    document.getElementById('expiration-date').addEventListener('input', function (e) {
      e.target.value = e.target.value.replace(/[^\dA-Z]/g, '').replace(/(.{2})/g, '$1 ').trim();
    });
    }
    

    //calcolo prezzo totale
    if (store.userCart) {
      for (let i = 0; i < store.userCart.dish.length; i++) {
        this.totalPrice.push(
          parseFloat(document.querySelector(`#price-${i}`).innerHTML)
        );
      }
      this.subtotal = this.totalPrice.reduce((pv, cv) => pv + cv, 0);

      // data locale
      const date = new Date();
      const formattedDate = date
        .toISOString()
        .replace(/T/, " ")
        .replace(/\..+/, "");
      this.orderData.order_date = formattedDate.toLocaleString();

      // codice random
      const min = 10000;
      const max = 99999;
      this.orderData.code = Math.floor(Math.random() * (max - min + 1)) + min;

      //prezzo totale
      this.shipping = parseFloat(document.getElementById("price").innerHTML);
      this.orderData.price = this.shipping + this.subtotal;
      // console.log(store.userCart.dish)

      // id piatti
      const ids = store.userCart.dish.map((element) => element.id);
      this.cartItems.dishesId = ids;
      // console.log(this.dishesId)
    }
  },
};
</script>

<template>
  <section class="pt-5">
    <div class="container pt-5">
      <div class="row d-flex justify-content-center my-4 my-cart">
        <div v-if="store.userCart" class="col-md-8">
          <div class="card my-card mb-4">
            <div class="card-header py-3" style="background: rgb(253, 187, 45)">
              <div>
                <h2 class="my-2 title">{{ this.rest.name }}</h2>
              </div>
              <div v-if="store.userCart.dish.length > 1">
                <h5 class="mb-0 title">
                  Carrello - {{ store.userCart.dish.length }} prodotti
                  selezionati
                </h5>
              </div>
              <div v-else-if="store.userCart.dish.length == 1">
                <h5 class="mb-0 title">
                  Carrello - {{ store.userCart.dish.length }} prodotto
                  selezionato
                </h5>
              </div>
              <div v-else-if="store.userCart.dish.length == 0">
                <h5 class="mb-0">Carrello - nessun prodotto selezionato</h5>
              </div>
            </div>
            <div class="card-body">
              <!-- PRODOTTO -->
              <div class="row" v-for="(item, index) in store.userCart.dish">
                <div class="col-lg-3 col-md-12 mb-4 mb-lg-0">
                  <!-- IMMAGINE -->
                  <div>
                    <img :src="item.img" class="img-fluid dish rounded-3" alt="item" />
                  </div>
                </div>

                <!-- NOME PRODOTTO -->
                <div class="col-lg-5 col-md-6 mb-4 mb-lg-0">
                  <p>
                    <strong>{{ item.name }}</strong>
                  </p>
                </div>

                <div class="col-lg-4 col-md-6 mb-4 mb-lg-0">
                  <!-- QUANTITA' -->
                  <div class="d-flex mb-4" style="max-width: 300px">
                    <button class="btn btn-quantity color-white px-3 me-2 mb-5" :id="'down-btn-' + index"
                      @click="QuantityDown(index, item.price)" disabled>
                      -
                    </button>

                    <div class="form-outline">
                      <input :id="'quantity-' + index" required min="1" max="11" :name="'quantity-' + index" value="1"
                        type="number" class="form-control" />
                      <label class="form-label" for="form1">Quantità</label>
                    </div>

                    <button class="btn btn-quantity color-white px-3 ms-2 mb-5" :id="'up-btn-' + index"
                      @click="QuantityUp(index, item.price)">
                      +
                    </button>
                  </div>

                  <!-- PREZZO -->
                  <div class="fw-bold price">
                    <span>€</span>
                    <div class="d-inline text-start text-md-center" :id="'price-' + index">
                      {{ item.price }}
                    </div>
                  </div>
                  <button class="btn btn-delete" @click="deleteCart(index)">
                    Elimina
                  </button>
                </div>
                <div v-if="index != store.userCart.dish.length - 1">
                  <hr class="mb-4" />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="d-flex flex-column align-items-center" v-else>
          <h2>Il carrello è vuoto!</h2>
          <img class="empty img-fluid" src="../assets/img/117-1170538_404-your-cart-is-empty.png" alt="empty">
        </div>

        <!-- RIEPILOGO ORDINE -->
        <div v-if="store.userCart" class="col-md-4">
          <div class="card mb-4 my-card">
            <div class="card-header py-3" style="background: rgb(253, 187, 45)">
              <h5 class="mb-0 title">Riepilogo ordine</h5>
            </div>
            <div class="card-body">
              <ul class="list-group list-group-flush">
                <li class="list-group-item d-flex justify-content-between align-items-center border-0 px-0 pb-0">
                  Subtotale
                  <span id="subtotal">{{ this.subtotal }}<span v-if="this.subtotal.toString().includes('.')">0</span><span
                      v-else>.00</span>
                    €</span>
                </li>
                <li class="list-group-item d-flex justify-content-between align-items-center px-0">
                  Prezzo di consegna
                  <span>{{ this.rest.price_shipping }}<span
                      v-if="this.rest.price_shipping.toString().includes('.')">0</span><span v-else>.00</span>
                    €</span>
                </li>
                <li class="list-group-item d-flex justify-content-between align-items-center border-0 px-0 mb-3">
                  <div>
                    <strong>Totale</strong>
                    <strong>
                      <p class="mb-0">(Iva inclusa)</p>
                    </strong>
                  </div>
                  <span>
                    <strong id="price">{{ parseFloat(this.subtotal) + parseFloat(this.rest.price_shipping) }}<span
                        v-if="parseFloat(this.subtotal) + parseFloat(this.rest.price_shipping).toString().includes('.')">0</span><span
                        v-else>.00</span>
                      €
                    </strong>
                  </span>
                </li>
              </ul>
              <!-- <button type="button" class="btn btn-primary btn-lg btn-block">Go to checkout</button> -->
              <button type="button" class="btn btn-primary btn-delete border-none" data-bs-toggle="modal"
                data-bs-target="#exampleModal" data-bs-whatever="@getbootstrap" @click="getQuantities">
                Vai all'ordine
              </button>

              <div class="modal modal-lg fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel"
                aria-hidden="true">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h1 class="modal-title fs-5" id="exampleModalLabel">
                        Inserisci i tuoi dati
                      </h1>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      <form class="w-75 mx-auto" @submit.prevent="addNewOrder()">
                        <div class="mb-3">
                          <label for="first-name" class="col-form-label">Nome*:</label>
                          <input type="text" class="form-control" id="first-name" v-model="orderData.firstname"
                            required />
                        </div>
                        <div class="mb-3">
                          <label for="last-name" class="col-form-label">Cognome*:</label>
                          <input type="text" class="form-control" id="last-name" v-model="orderData.lastname" required />
                        </div>
                        <div class="mb-3">
                          <label for="address" class="col-form-label">Indirizzo*:</label>
                          <input type="text" class="form-control" id="address" v-model="orderData.address" required />
                        </div>
                        <div class="mb-3">
                          <label for="email" class="col-form-label">Email*:</label>
                          <input type="email" class="form-control" id="email" v-model="orderData.email" required />
                        </div>
                        <div class="mb-3">
                          <label for="phone-number" class="col-form-label">Numero di telefono*:</label>
                          <input type="text" class="form-control" id="phone-number" pattern="[0-9]+"
                            v-model="orderData.phone_number" required />
                        </div>
                        <div class="mb-3">
                          <label for="info" class="col-form-label">Informazioni aggiuntive:</label>
                          <textarea type="textarea" class="form-control" id="info"
                            placeholder="Aggiungi informazioni che possono esserci utili"
                            v-model="orderData.additional_info"></textarea>

                          <div class="border mt-5">
                            <div class="border-bottom d-flex justify-content-between p-2 ps-3 pe-4">
                              <div class="d-flex">
                                <img style="width:30px"
                                  src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiPjxwYXRoIGQ9Ik0yMiAzYy41MyAwIDEuMDM5LjIxMSAxLjQxNC41ODZzLjU4Ni44ODQuNTg2IDEuNDE0djE0YzAgLjUzLS4yMTEgMS4wMzktLjU4NiAxLjQxNHMtLjg4NC41ODYtMS40MTQuNTg2aC0yMGMtLjUzIDAtMS4wMzktLjIxMS0xLjQxNC0uNTg2cy0uNTg2LS44ODQtLjU4Ni0xLjQxNHYtMTRjMC0uNTMuMjExLTEuMDM5LjU4Ni0xLjQxNHMuODg0LS41ODYgMS40MTQtLjU4NmgyMHptMSA4aC0yMnY4YzAgLjU1Mi40NDggMSAxIDFoMjBjLjU1MiAwIDEtLjQ0OCAxLTF2LTh6bS0xNSA1djFoLTV2LTFoNXptMTMtMnYxaC0zdi0xaDN6bS0xMCAwdjFoLTh2LTFoOHptLTEwLTZ2MmgyMnYtMmgtMjJ6bTIyLTF2LTJjMC0uNTUyLS40NDgtMS0xLTFoLTIwYy0uNTUyIDAtMSAuNDQ4LTEgMXYyaDIyeiIvPjwvc3ZnPg==">
                                <div class="px-3">Pagamento</div>
                              </div>
                              <div>
                                <img class="mx-2" style="width:45px" width="45"
                                  src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Visa_Inc._logo.svg" alt="">
                                <img class="mx-2" style="width:35px"
                                  src="https://upload.wikimedia.org/wikipedia/commons/2/2a/Mastercard-logo.svg" alt="">
                                <img class="mx-2" style="width:40px"
                                  src="https://upload.wikimedia.org/wikipedia/commons/1/1b/UnionPay_logo.svg" alt="">
                                <img class="mx-2" style="width:30px"
                                  src="https://upload.wikimedia.org/wikipedia/commons/f/fa/American_Express_logo_%282018%29.svg"
                                  alt="">
                                <img class="mx-2 me-0" style="width:40px"
                                  src="https://upload.wikimedia.org/wikipedia/commons/4/40/JCB_logo.svg" alt="">
                              </div>
                            </div>
                            <div class="p-3 my-3">
                              <label for="card-number">Numero carta</label>
                              <input id="card-number" class="mb-3 shadow-none form-control" type="text" maxlength="19"
                                onkeypress="return (event.charCode !=8 && event.charCode ==0 || (event.charCode >= 48 && event.charCode <= 57))"
                                placeholder="**** **** **** ****" required>

                              <label for="expiration-date">Data di scadenza</label>
                              <input id="expiration-date" class="mb-3 shadow-none form-control" type="text" maxlength="5"
                                onkeypress="return (event.charCode !=8 && event.charCode ==0 || (event.charCode >= 48 && event.charCode <= 57))"
                                placeholder="MM/YY" required>
                            </div>
                          </div>
                        </div>

                        <div class="d-flex justify-content-end mt-2">
                          <button id="submit-button" class="button button--small button--green mx-3">
                            Conferma ordine</button>
                          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                            Chiudi
                          </button>
                          <!-- <button type="submit" class="btn btn-delete">
                                    <router-link
                                    class="text-decoration-none text"
                                    :to="{ name: 'ordine' }"
                                    >
                                    Conferma ordine
                                </router-link>
                            </button> -->
                        </div>
                      </form>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>

section {
  min-height: calc( 100vh - 340.19px);
}
.title {
  color: white;
}

.empty{
  
}

.btn-quantity {
  background-color: rgba(195, 34, 34);
  color: white;
}

.price {
  position: relative;
  top: -20px;
}

.text {
  color: white;
}

.btn-delete {
  background-color: rgb(253, 187, 45);
  color: white;
  border: none;
}

img {
  width: 300px;
}

.button {
  cursor: pointer;
  font-weight: 500;
  left: 3px;
  line-height: inherit;
  position: relative;
  text-decoration: none;
  text-align: center;
  border-style: solid;
  border-width: 1px;
  border-radius: 3px;
  display: inline-block;
}

.button--small {
  padding: 10px 20px;
  font-size: 0.875rem;
}

.button--green {
  outline: none;
  background-color: #64d18a;
  border-color: #64d18a;
  color: white;
  transition: all 200ms ease;
}

.button--green:hover {
  background-color: #8bdda8;
  color: white;
}

.my-cart {
  padding-top: 125px;
}

.my-card {
  border-color: rgba(195, 34, 34);
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}
input[type="number"] {
    -moz-appearance: textfield;
}
</style>
