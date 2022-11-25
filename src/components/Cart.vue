<template>
    <div class="cart">
        <div v-if="!cart.length" class="alert alert-secondary" role="alert">
            No product in cart!
        </div>
        <div v-if="orderPlaced" class="alert alert-success" role="alert">
            Order successfully placed!
            <button
                type="button"
                class="btn-close me-0"
                data-bs-dismiss="modal"
                aria-label="Close"
                @click="() => (orderPlaced = false)"
            ></button>
        </div>
        <ul class="list-group">
            <li class="list-group-item" v-for="item in cart" :key="item.id">
                <div class="row">
                    <div class="col-md-4">
                        <img
                            width="80px"
                            :src="item.imgUrl"
                            class="mr-3"
                            :alt="item.title"
                        />
                    </div>
                    <div class="col-md-7">
                        <p class="mt-0">
                            {{ item.title }}
                        </p>
                        <button
                            @click="reduceQty(item.id)"
                            class="btn-qty btn btn-sm btn-secondary"
                        >
                            -
                        </button>
                        x {{ item.qty }}
                        <button
                            @click="addQty(item.id)"
                            class="btn-qty btn btn-sm btn-secondary"
                        >
                            +
                        </button>
                    </div>
                    <div class="col-md-1">
                        <button
                            @click="removeItem(item.id)"
                            type="button"
                            class="btn-close"
                            aria-label="Close"
                        ></button>
                    </div>
                </div>
            </li>
        </ul>
        <button
            class="btn btn-checkout btn-lg btn-block btn-success"
            v-if="cart.length"
            :disabled="isProcessing"
            @click="placeOrder"
        >
            <span v-if="!isProcessing">Checkout ($ {{ totalPrice }})</span>

            <div v-else class="spinner-border" role="status">
                <span class="visually-hidden">Loading...</span>
            </div>
        </button>
    </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
    name: "Cart",
    data() {
        return {
            isProcessing: false,
            orderPlaced: false,
        };
    },
    computed: {
        ...mapGetters(["cart"]),
        totalPrice() {
            return this.cart.reduce((a, b) => a + b.qty * b.price, 0);
        },
    },
    methods: {
        ...mapActions(["addQty", "reduceQty", "removeItem", "emptyCart"]),
        placeOrder() {
            this.isProcessing = true;
            setTimeout(() => {
                this.orderPlaced = true;
                this.isProcessing = false;
                this.emptyCart();
            }, 1000);
        },
    },
};
</script>

<style scoped>
.btn-qty {
    border-radius: 50%;
    width: 30px;
}

.btn-checkout {
    margin-top: 20px;
}
</style>