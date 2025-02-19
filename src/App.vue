<template>
  <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

  <div v-for="(item, index) in products" :key="item.title">
    <h4>{{ item.title }}</h4>
    <p>{{ item.price }}</p>
  </div>
</template>
<style scope>
body {
  text-align: center;
}
</style>

<script>
export default {
  name: "App",
  data() {
    return {
      price1: 60,
      price2: 70,
      style: "color : red",
      products: [
        { title: "역삼동원룸", price: "50만원" },
        { title: "천호동원룸", price: "가격은아무거나" },
        { title: "마포구원룸", price: "가격은아무거나" },
      ],
    };
  },
  components: {},
};
</script>
