<template>
    <div id="app">
        <Header />
        <div class="container">
            <div class="row">
                <div class="col-md-8">
                    <ProductList />
                </div>
                <div class="col-md-4">
                    <Cart />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Header from "@/components/Header.vue";
import ProductList from "@/components/ProductList.vue";
import Cart from "@/components/Cart.vue";

export default {
    name: "App",
    components: {
        Header,
        ProductList,
        Cart,
    },
};
</script>