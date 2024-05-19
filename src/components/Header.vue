<script setup>
const props = defineProps({
    cart: {
        type: Array,
        required: true,
    },
});

</script>

<template>
    <header class="py-5 header">
        <div class="container-xl">
            <div class="row justify-content-center justify-content-md-between">
                <div class="col-8 col-md-3">
                    <a href="index.html">
                        <img class="img-fluid" src="/img/logo.svg" alt="imagen logo" />
                    </a>
                </div>
                <nav class="col-md-6 a mt-5 d-flex align-items-start justify-content-end">
                    <div class="cart">
                        <img class="img-fluid" src="/img/cart.png" alt="Cart" />

                        <div id="cart" class="bg-white p-3">
                            <p v-if="cart.length === 0" class="text-center m-0">
                                The shopping cart is empty
                            </p>
                            <div v-else>
                                <table class="w-100 table">
                                    <thead>
                                        <tr>
                                            <th>Image</th>
                                            <th>Name</th>
                                            <th>Price</th>
                                            <th>Quantity</th>
                                            <th></th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr v-for="guitar in cart">
                                            <td>
                                                <img class="img-fluid" :alt="guitar.name"
                                                    :src="'/img/' + guitar.image + '.jpg'" />
                                            </td>
                                            <td>{{ guitar.name }}</td>
                                            <td class="fw-bold">${{ guitar.price }}</td>
                                            <td class="flex align-items-start gap-4">
                                                <button type="button" class="btn btn-dark">-</button>
                                                {{ guitar.quantity }}
                                                <button type="button" class="btn btn-dark">+</button>
                                            </td>
                                            <td>
                                                <button class="btn btn-danger" type="button">X</button>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>

                                <p class="text-end">
                                    Totalprice: <span class="fw-bold">$899</span>
                                </p>
                                <button class="btn btn-dark w-100 mt-3 p-2">Clear cart</button>
                            </div>
                        </div>
                    </div>
                </nav>
            </div>
            <!--.row-->

            <div class="row mt-5">
                <div class="col-md-6 text-center text-md-start pt-5">
                    <h1 class="display-2 fw-bold">Modelo VAI</h1>
                    <p class="mt-5 fs-5 text-white">
                        Lorem ipsum dolor sit amet consectetur adipisicing elit. Temporibus,
                        possimus quibusdam dolor nemo velit quo, fuga omnis, iure molestias
                        optio tempore sint at ipsa dolorum odio exercitationem eos inventore
                        odit.
                    </p>
                    <p class="text-primary fs-1 fw-black">$399</p>
                    <button type="button" class="btn fs-4 bg-primary text-white py-2 px-5">
                        Add to the cart
                    </button>
                </div>
            </div>
        </div>

        <img class="header-guitar" src="/img/header_guitar.png" alt="imagen header" />
    </header>
</template>
