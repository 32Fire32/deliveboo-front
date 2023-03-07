<script>
export default {
  name: "Order",
};
</script>

<template>
  <div class="container">
    <div class="order">
      <h5> <b>Il tuo ordine è stato ricevuto</b> </h5>
    <i class="fa-solid fa-circle-check space"></i>
    <p>Grazie per il tuo acquisto!</p>
    <small>Verrà contattato a breve dal ristoratore per la conferma del suo ordine.</small>
    <router-link class="text-decoration-none text-center text-white nav-link mx-2 m-0 py-2 my-hamburger"
                :to="{ name: 'homepage' }"><span>Torna al sito</span></router-link>
    </div>
  </div>
    
</template>

<style lang="scss" scoped>
.order{
  padding-top: 250px;
  min-height: calc(100vh - 340.19px);
  display:flex;
  flex-direction: column;
  align-items: center;
}

small {
  margin-bottom: 10px;
}

.my-hamburger{
  background-color: rgb(253, 187, 45);
  border-radius: 10px;
  width: 10%;
}

.space {
  color: green;
  font-size: 50px;
  padding: 10px;
}
</style>
