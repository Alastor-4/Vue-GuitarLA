<script setup>
import { onMounted, ref } from 'vue';
import { db } from './data/guitars.js';
import Guitar from './components/Guitar.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';

const guitars = ref([]);
const cart = ref([]);

onMounted(() => {
  guitars.value = db;
})

const addToCart = (guitar) => {
  const alreadyExist = cart.value.findIndex(product => product.id === guitar.id);
  if (alreadyExist >= 0) {
    cart.value[alreadyExist].quantity++;
  } else {
    guitar.quantity = 1;
    cart.value.push(guitar);
  }
}

</script>

<template>
  <Header :cart="cart" />

  <main class="container-xl mt-5">
    <h2 class="text-center">Our Collection</h2>

    <div class="row mt-5">
      <Guitar v-for="guitar in guitars" :guitar="guitar" @click="addToCart(guitar)" />
    </div>
  </main>

  <Footer />

</template>