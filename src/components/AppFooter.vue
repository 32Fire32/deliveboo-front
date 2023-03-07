<script>
export default {
  name: "AppFooter",
};
</script>

<template>
  <!-- Remove the container if you want to extend the Footer to full width. -->
  <!-- <svg class="my-rotate" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1440 320" data-v-2d1117dc="">
                                          <path fill="#fdbb2d" fill-opacity="1"
                                            d="M0,128L40,144C80,160,160,192,240,197.3C320,203,400,181,480,154.7C560,128,640,96,720,85.3C800,75,880,85,960,112C1040,139,1120,181,1200,192C1280,203,1360,181,1400,170.7L1440,160L1440,0L1400,0C1360,0,1280,0,1200,0C1120,0,1040,0,960,0C880,0,800,0,720,0C640,0,560,0,480,0C400,0,320,0,240,0C160,0,80,0,40,0L0,0Z"
                                            data-v-2d1117dc=""></path>
                                        </svg> -->
  <div class="my-footer">

    <!-- Footer -->
    <footer class="text-center text-white">
      <!-- Grid container -->
      <div class="container p-4 pb-0">
        <!-- Section: Links -->
        <section class="">
          <!--Grid row-->
          <div class="row">
            <!-- Grid column -->
            <div class="col-md-3 col-lg-3 col-xl-3 mx-auto mt-3 my-column-footer">
              <h6 class="text-uppercase mb-4 my-font">Scopri Deliveroo</h6>
              <small>
                <a href="/chi-siamo" class="my-link">Investitori</a> <br />
                <a href="/chi-siamo" class="my-link">Chi siamo</a> <br />
                <a href="/ristoranti" class="my-link">Ristoranti</a> <br />
                <a href="/" class="my-link">Altro</a> <br />
                <a href="/chi-siamo" class="my-link">Lavora con noi</a> <br />
                <a href="/chi-siamo" class="my-link">Diventa nostro partner</a>
              </small>
            </div>
            <!-- Grid column -->

            <hr class="w-100 clearfix d-md-none" />

            <!-- Grid column -->
            <div class="col-md-2 col-lg-2 col-xl-2 mx-auto mt-3 my-column-footer">
              <h6 class="text-uppercase mb-4 my-font">Note legali</h6>
              <small>
                <a href="" class="my-link">Termini & Condizioni</a> <br />
                <a href="" class="my-link">Informativa sulla privacy</a> <br />
                <a href="" class="my-link">Cookies</a>
              </small>
            </div>
            <!-- Grid column -->

            <hr class="w-100 clearfix d-md-none" />

            <!-- Grid column -->
            <div class="col-md-3 col-lg-2 col-xl-2 mx-auto mt-3 my-column-footer">
              <h6 class="text-uppercase mb-4 my-font">Contatti</h6>
              <small>
                <a href="https://www.google.it/maps/place/Deliveroo+-+Uffici/@45.440727,9.1550847,15z/data=!3m1!4b1!4m5!3m4!1s0x4786c3eb2e46548f:0x41f8390b6101381c!8m2!3d45.4407273!4d9.163818"
                  class="my-link">Indirizzo</a>
                <br />
                <a href="" class="my-link">+39 3476589065</a> <br />
                <a href="" class="my-link">800 666 898</a> <br />
                <a href="" class="my-link">help@deliveboo.com</a>
              </small>
            </div>

            <!-- Grid column -->
            <hr class="w-100 clearfix d-md-none" />

            <!-- Grid column -->
            <div class="col-md-4 col-lg-3 col-xl-3 mx-auto mt-3 my-column-footer">
              <h6 class="text-uppercase mb-4 my-font">Social</h6>

              <small>
                <p>
                  <a href="https://it-it.facebook.com/" class="text-white"><i
                      class="fa-brands fa-facebook my-social"></i></a>
                </p>
                <p>
                  <a href="https://www.instagram.com/" class="text-white"><i
                      class="fa-brands fa-instagram my-social"></i></a>
                </p>
                <p>
                  <a href="https://www.tiktok.com/login?redirect_url=https%3A%2F%2Fwww.tiktok.com%2Fit-IT&lang=en&enter_method=mandatory"
                    class="text-white"><i class="fa-brands fa-tiktok my-social"></i></a>
                </p>
                <p>
                  <a href="https://twitter.com/?lang=it" class="text-white"><i
                      class="fa-brands fa-twitter my-social"></i></a>
                </p>
              </small>
            </div>
            <!-- Grid column -->
          </div>
          <!--Grid row-->
        </section>
        <!-- Section: Links -->

        <hr class="my-3" />

        <!-- Section: Copyright -->
        <section class="p-3 pt-0">
          <div class="row d-flex my-column-footer">
            <!-- Grid column -->
            <div>
              <!-- Copyright -->
              <div class="p-3">
                © 2023 Copyright:
                <a class="text-white" href="">Deliveboo.com</a>
              </div>
              <!-- Copyright -->
            </div>
            <!-- Grid column -->

            <!-- Grid column -->
          </div>
        </section>
        <!-- Section: Copyright -->
      </div>
      <!-- Grid container -->
    </footer>
    <!-- Footer -->
  </div>
  <!-- End of .container -->
</template>

<style lang="scss" scoped>
a:hover,
h6:hover {
  cursor: pointer;
  color: rgb(158, 15, 15);
  // height: 100%;

}

.my-footer {
  // position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background: rgb(253, 187, 45);
}

.my-font {
  font-weight: 800;
}

.my-link {
  color: white;
  text-decoration: none;
}

.my-social {
  font-size: 20px;
}
</style>
