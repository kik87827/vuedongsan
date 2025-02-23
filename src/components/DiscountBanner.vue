<template>
  <div class="discount">
    <h4>지금 결제하면 {{ percentData }}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: "DiscountBanner",
  data() {
    return {
      discountTimer: 0,
      percentData: 20,
    };
  },
  mounted() {
    this.percentCounter();
  },
  unmounted() {
    clearInterval(this.discountTimer);
    this.discountTimer = 0;
  },
  methods: {
    percentCounter() {
      this.discountTimer = setInterval(() => {
        if (this.percentData > 0) {
          this.percentData -= 1;
        }
      }, 1000);
    },
  },
  components: {},
};
</script>

<style scoped></style>
