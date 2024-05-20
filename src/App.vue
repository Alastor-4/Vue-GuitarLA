<script setup>
import { onMounted, ref, watch } from "vue";
import { db } from "./data/guitars.js";
import Guitar from "./components/Guitar.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

const guitars = ref([]);
const cart = ref([]);
const guitar = ref({});

watch(
  cart,
  () => {
    setStorageCart();
  },
  { deep: true }
);

onMounted(() => {
  guitars.value = db;
  guitar.value = db[3];

  const storageCart = localStorage.getItem("cart");
  if (storageCart) {
    cart.value = JSON.parse(storageCart);
  }
});

const setStorageCart = () => {
  localStorage.setItem("cart", JSON.stringify(cart.value));
};

const addToCart = (guitar) => {
  const alreadyExist = cart.value.findIndex(
    (product) => product.id === guitar.id
  );

  if (alreadyExist >= 0) {
    cart.value[alreadyExist].quantity++;
  } else {
    guitar.quantity = 1;
    cart.value.push(guitar);
  }
};

const increaseQuantity = (id) => {
  const index = cart.value.findIndex((product) => product.id === id);
  if (cart.value[index].quantity >= 5) return;
  cart.value[index].quantity++;
};

const decreaseQuantity = (id) => {
  const index = cart.value.findIndex((product) => product.id === id);
  if (cart.value[index].quantity <= 1) return;
  cart.value[index].quantity--;
};

const deleteProduct = (id) => {
  cart.value = cart.value.filter((product) => product.id !== id);
};

const deleteAllProducts = () => {
  cart.value = [];
};
</script>

<template>
  <Header
    :cart="cart"
    :guitar="guitar"
    @addToCart="addToCart"
    @increaseQuantity="increaseQuantity"
    @decreaseQuantity="decreaseQuantity"
    @deleteProduct="deleteProduct"
    @deleteAllProducts="deleteAllProducts"
  />

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra colección</h2>

    <div class="row mt-5">
      <Guitar
        v-for="guitar in guitars"
        :guitar="guitar"
        @click="addToCart(guitar)"
      />
    </div>
  </main>

  <Footer />
</template>
