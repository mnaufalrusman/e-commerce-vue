<template>
  <nav class="navbar navbar-expand bg-light">
    <div class="navbar-text ms-auto mx-3 d-flex">
      <button
        class="btn btn-sm btn-outline-success"
        @click="$emit('toggle-slide')"
      >
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="dropdown ms-3" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="dropdownCart"
          data-bs-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge rounded-pill text-bg-success">{{ cartQty }}</span>
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
          <price :value="Number(cartTotal)"></price>
        </button>
        <div
          class="dropdown-menu dropdown-menu-end"
          aria-labelledby="dropdownCart"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-wrap text-end">
              <span
                class="badge rounded-pill text-bg-warning align-text-top me-1"
              >
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>{{ (item.product.price * item.qty) | currencyFormat }}</b>
              <a
                href="#"
                class="badge bg-danger text-white"
                @click.stop="$emit('delete-item', index)"
                >-</a
              >
            </div>
          </div>
          <router-link
            class="btn btn-sm btn-outline-info text-dark float-end me-2"
            to="/checkout"
            >Checkout</router-link
          >
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./Price.vue";

export default {
  name: "navbar",
  components: {
    FontAwesomeIcon,
    Price,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "Rp" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
