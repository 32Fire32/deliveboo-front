<script>
import { store } from "../store";
export default {
  name: "AppHeader",
  data() {
    return {
      store,
    };
  },
};
$(document).ready(function () {
  $("nav ul li a:not(:only-child)").click(function (e) {
    $(this).siblings(".nav-dropdown").toggle();
    e.stopPropagation();
  });

  $("html").click(function () {
    $(".nav-dropdown").hide();
  });
  $("#nav-toggle").click(function () {
    $("nav ul").slideToggle();
  });
  $("#nav-toggle").on("click", function () {
    this.classList.toggle("active");
  });
});
</script>

<template>
  <div class="all-header">
    <div class="img-preheader"></div>
    <div class="nav-bar">
      <div class="nav-container">
        <div class="brand">
          <a href="/"><img class="img-fluid my-img" src="../assets/img/delivebo-fork.png" alt="" /></a>
        </div>
        <nav>
          <div class="nav-mobile">
            <a href="#" id="nav-toggle">
              <span></span>
            </a>
          </div>
          <ul class="nav-list">
            <li class="nav-item">
              <router-link class="text-decoration-none text-white nav-link mx-2 m-0 py-2 my-hamburger"
                :to="{ name: 'homepage' }"><span>Home</span></router-link>
            </li>
            <li class="nav-item">
              <router-link class="text-decoration-none text-white nav-link mx-2 m-0 py-2 my-hamburger"
                :to="{ name: 'restaurant-sponsored' }"><span>Consigliati</span></router-link>
            </li>
            <li class="nav-item view">
              <router-link class="text-decoration-none text-white nav-link mx-2 m-0 py-2 my-hamburger"
                :to="{ name: 'about-us' }"><span> Chi siamo</span></router-link>
            </li>
            <li class="nav-item">
              <router-link
                class="text-decoration-none text-white nav-link mx-2 m-0 py-2 my-hamburger btn position-relative"
                style="background: rgba(195, 34, 34)" :to="{ name: 'checkout' }"><i
                  class="fa-solid fa-cart-shopping my-cart"></i>
                <span v-if="store.userCart.dish"
                  class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                  {{ store.userCart.dish.length }}
                  <span class="visually-hidden">unread messages</span>
                </span></router-link>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.my-img {
  width: 140px;
  margin-top: -30px;
  margin-left: -10px;
}

.nav-bar {
  height: 70px;
  background: rgb(253, 187, 45);
  border-top: 2px solid rgba(195, 34, 34);
  border-bottom: 2px solid rgba(195, 34, 34);
  box-shadow: 0px 0px 5px 2px rgb(0 0 0 / 20%);
}

.my-hamburger {
  padding-right: 20px;
}

.brand {
  float: left;
  position: absolute;
  padding-left: 20px;
  line-height: 70px;
  font-size: 1.5em;
}

.brand a {
  text-decoration: none;
  color: white;
}

.nav-container {
  max-width: 1000px;
  margin: 0 auto;
}

nav {
  float: right;
}

nav ul {
  list-style: none;
}

nav ul li {
  float: left;
  position: relative;
}

nav ul li a {
  display: block;
  padding: 0 20px;
  line-height: 50px;
  background: rgb(253, 187, 45);
  margin-top: 8px;
  font-size: 20px;
  text-decoration: none;
  color: #fff;
}

// nav ul li a:hover{
//     background: #2ab1ce;
//     color: #fff;
// }

nav ul li a:not(:only-child):after {
  content: "▼";
  padding-left: 5px;
}

nav ul li ul li {
  min-width: 190px;
}

nav ul li ul li a {
  padding: 15px;
  line-height: 20px;
}

.nav-dropdown {
  position: absolute;
  display: none;
  z-index: 1;
}

.nav-mobile {
  display: none;
  position: absolute;
  top: 0;
  right: 0;
  height: 70px;
  width: 70px;
}

#nav-toggle {
  position: absolute;
  left: 18px;
  top: 22px;
  cursor: pointer;
  padding: 10px 35px 15px 0px;
}

#nav-toggle span,
#nav-toggle span::before,
#nav-toggle span::after {
  position: absolute;
  display: block;
  content: "";
  background: #fff;
  height: 5px;
  width: 35px;
  transition: all 300ms ease-in-out;
}

#nav-toggle span::before {
  top: -10px;
}

#nav-toggle span::after {
  bottom: -10px;
}

#nav-toggle.active span {
  background-color: transparent;
}

#nav-toggle.active span::before,
#nav-toggle.active span::after {
  top: 0;
}

#nav-toggle.active span::before {
  transform: rotate(45deg);
}

#nav-toggle.active span::after {
  transform: rotate(-45deg);
}

li:hover span {
  border-bottom: 2px solid rgb(173, 121, 7);
  // height: 100%;
  padding-bottom: 5px;
  border-radius: 5px;
}

@media only screen and (max-width: 799px) {
  .img-preheader {
    display: none;
  }

  .img-none {
    display: none;
  }

  .nav-mobile {
    display: block;
  }

  nav {
    width: 100%;
    padding: 70px 0 15px;
  }

  nav ul {
    display: none;
  }

  nav ul li {
    float: none;
  }

  nav ul li a {
    // padding: 15px;
    // line-height: 20px;
    // padding-left: 25%;
  }

  nav ul li ul li a {
    padding-left: 30%;
  }

  .nav-dropdown {
    position: static;
  }

  .brand {
    display: block;
  }

  .nav-list {
    width: 200px;
    margin-left: auto;
    text-align: center;
  }
}

.nav-bar {
  display: block;
}

@media screen and (min-width: 800px) {
  .nav-list {
    display: block !important;
  }

  .brand {
    display: none;
  }

  .nav-bar {
    display: flex;
  }
}

.all-header {
  position: fixed;
  width: 100%;
  z-index: 1;
}

.img-preheader {
  background-image: url(https://thumbs.dreamstime.com/b/banner-sweet-potato-chips-flat-lay-view-website-header-fast-food-restaurants-136423838.jpg);
  // https://thumbs.dreamstime.com/b/banner-sweet-potato-chips-flat-lay-view-website-header-fast-food-restaurants-136423838.jpg
  // https://www.freewebheaders.com/wp-content/gallery/food/delicious-orange-salmon-caviar-website-header.jpg
  // https://www.freewebheaders.com/wp-content/gallery/food/french-fries-natural-food-website-header-image.jpg
  background-size: cover;
  height: 70px;
  background-repeat: no-repeat;
  position: relative;
}

.my-cart {
  font-size: 20px;
}
</style>
