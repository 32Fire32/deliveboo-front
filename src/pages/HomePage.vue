<script>
import CategoryList from "../components/CategoryList.vue";
export default {
  name: "HomePage",
  components: {
    CategoryList,
  },
};
</script>

<template>
  <div class="my-container">
    <!-- ======= Hero Section ======= -->
    <section id="hero" class="container hero d-flex align-items-center section-bg">
      <div class="container my-container2">
        <div class="row justify-content-center gy-5 my-hero">
          <div
            class="col-lg-5 order-2 order-lg-1 d-flex flex-column justify-content-center align-items-center align-items-lg-start text-center text-lg-start">
            <img class="img-fluid logo-hero" src="../assets/img/delivebo-fork.png" alt="" />
            <h2 data-aos="fade-up">
              I piatti dei ristoranti che ami, a domicilio
            </h2>
            <p data-aos="fade-up" data-aos-delay="100">
              Approfitta di un'ampia varietà di ristoranti per ordinare i tuoi
              piatti preferiti e gustarli direttamente a casa tua!
            </p>
          </div>
          <div class="col-lg-5 order-1 order-lg-2 text-center text-lg-start">
            <img src="src\assets\img\PIZZA HERO_preview_rev_1.png" class="img-fluid rotate" alt="" data-aos="zoom-out"
              data-aos-delay="300" />
          </div>
        </div>
      </div>
    </section>
  </div>
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 80 1440 200">
    <path fill="#fdbb2d" fill-opacity="1"
      d="M0,128L40,144C80,160,160,192,240,197.3C320,203,400,181,480,154.7C560,128,640,96,720,85.3C800,75,880,85,960,112C1040,139,1120,181,1200,192C1280,203,1360,181,1400,170.7L1440,160L1440,0L1400,0C1360,0,1280,0,1200,0C1120,0,1040,0,960,0C880,0,800,0,720,0C640,0,560,0,480,0C400,0,320,0,240,0C160,0,80,0,40,0L0,0Z">
    </path>
  </svg>
  <!-- End Hero Section -->
  <div>
    <CategoryList class="text-center" />
  </div>
  <svg class="my-rotate" xmlns="http://www.w3.org/2000/svg" viewBox="0 80 1440 200" data-v-2d1117dc="">
    <path fill="#fdbb2d" fill-opacity="1"
      d="M0,128L40,144C80,160,160,192,240,197.3C320,203,400,181,480,154.7C560,128,640,96,720,85.3C800,75,880,85,960,112C1040,139,1120,181,1200,192C1280,203,1360,181,1400,170.7L1440,160L1440,0L1400,0C1360,0,1280,0,1200,0C1120,0,1040,0,960,0C880,0,800,0,720,0C640,0,560,0,480,0C400,0,320,0,240,0C160,0,80,0,40,0L0,0Z"
      data-v-2d1117dc=""></path>
  </svg>
</template>

<style lang="scss" scoped>
/*--------------------------------------------------------------
# Hero Section
--------------------------------------------------------------*/
.my-rotate {
  transform: rotate(180deg);
}

.my-container {
  background-color: rgb(253, 187, 45);
}

.hero {
  width: 100%;
  background-size: cover;
  position: relative;
  min-height: 60vh;
  padding: 100px 0 60px 0;
}

.my-hero {
  margin: 60px;
}

.hero h2 {
  font-size: 64px;
  font-weight: 700;
  margin-bottom: 20px;
  color: rgb(195, 34, 34);
}

.hero h2 span {
  color: var(--color-primary);
}

.hero p {
  color: white;
  font-weight: 200;
  margin-bottom: 30px;
  font-style: italic;
  font-size: 18px;
}

.hero .btn-book-a-table {
  font-weight: 500;
  font-size: 14px;
  letter-spacing: 1px;
  display: inline-block;
  padding: 12px 36px;
  border-radius: 50px;
  transition: 0.5s;
  color: #fff;
  background: var(--color-primary);
  box-shadow: 0 8px 28px rgba(206, 18, 18, 0.2);
}

.hero .btn-book-a-table:hover {
  background: rgba(206, 18, 18, 0.8);
  box-shadow: 0 8px 28px rgba(206, 18, 18, 0.45);
}

.hero .btn-watch-video {
  font-size: 16px;
  transition: 0.5s;
  margin-left: 25px;
  color: var(--font-secondary);
  font-weight: 600;
}

.hero .btn-watch-video i {
  color: var(--color-primary);
  font-size: 32px;
  transition: 0.3s;
  line-height: 0;
  margin-right: 8px;
}

.hero .btn-watch-video:hover {
  color: var(--color-primary);
}

.hero .btn-watch-video:hover i {
  color: rgba(206, 18, 18, 0.8);
}

.logo-hero {
  width: 300px;
  margin-top: -100px;
  margin-bottom: -100px;
}

@media (max-width: 768px) {
  .hero h2 {
    font-size: 36px;
  }

  .hero .btn-get-started,
  .hero .btn-watch-video {
    font-size: 14px;
  }

  .logo-hero {
    display: none;
  }

  .hero {
    padding: 130px 0 60px 0;
  }

  .hero h2 {
    font-size: 25px;
  }

  h2 {
    margin-top: -40px;
  }

  .my-container2 {
    margin-top: -160px;
  }
}

.rotate {
  animation: rotation 100s infinite linear;
}

@keyframes rotation {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(359deg);
  }
}
</style>
