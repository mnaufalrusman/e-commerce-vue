<template>
  <transition
    name="custom"
    enter-active-class="animated fadeInDown"
    leave-active-class="animated slideOutRight"
  >
    <div v-if="sliderStatus">
      <div class="row g-3 align-items-center" :class="sliderState">
        <div class="col-auto">
          <label for="" class="font-weight-bold me-2">Max</label>
        </div>
        <div class="col-auto">
          <input
            type="number"
            class="form-control mx-2"
            style="width: 60px; text-align: center"
            v-model="maxAmount"
            @change="$emit('update:maximum', maxAmount)"
          />
        </div>
        <div class="col-8">
          <input
            type="range"
            class="form-range"
            min="0"
            max="200"
            v-model="maxAmount"
            @input="$emit('update:maximum', maxAmount)"
          />
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function () {
    return {
      maxAmount: 50,
    };
  },
  props: ["sliderStatus", "maximum"],
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>

<style>
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease-in-out;
}
</style>
