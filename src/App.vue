<template>
  <div class="black-bg" v-if="modalToggle">
    <div class="white-bg">
      <img :src="`/room${modalIndex}.jpg`" class="room-img" alt="" />
      <h4>{{ products[modalIndex].title }}</h4>
      <p>{{ products[modalIndex].price }}</p>
      <div><button @click="modalToggle = false">닫기</button></div>
    </div>
  </div>

  <div class="menu">
    <a v-for="(item, index) in menus" :key="item">{{ item }}</a>
  </div>
  <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->

  <div v-for="(item, index) in products" :key="item.title" class="room-list">
    <img :src="`/room${index}.jpg`" class="room-img" alt="" />
    <h4 @click="modalOpen(index)">{{ item.title }}</h4>
    <p>{{ item.price }}</p>
    <div>
      <button @click="countUp(index)">허위매물신고</button> <span>신고수 : {{ count[index] }}</span>
    </div>
  </div>
</template>
<style scope>
body {
  margin: 0;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
  text-align: center;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
.room-list {
  text-align: center;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
  box-sizing: border-box;
  top: 0;
  left: 0;
}
.white-bg {
  width: 100%;
  background: #fff;
  border-radius: 8px;
  box-sizing: border-box;
  padding: 20px;
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
      menus: ["Home", "Products", "About"],
      count: [],
      modalToggle: false,
      modalIndex: 0,
    };
  },
  components: {},
  methods: {
    countUp(index) {
      this.count[index] += 1;
    },
    modalOpen(index) {
      this.modalToggle = true;
      this.modalIndex = index;
    },
  },
  mounted() {},
  created() {
    this.products.forEach(() => this.count.push(0));
  },
};
</script>
