<template>
  <div class="menu">
    <a v-for="(item, index) in menus" :key="item">{{ item }}</a>
  </div>
  <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->

  <div v-for="(item, index) in products" :key="item.title">
    <img src="./assets/room0.jpg" class="room-img" alt="">
    <h4>{{ item.title }}</h4>
    <p>{{ item.price }}</p>
    <div>
      <button @click="countUp(index)">허위매물신고</button> <span>신고수 : {{ count[index] }}</span>
    </div>
  </div>
</template>
<style scope>
body {
  text-align: center;
}
.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img{width:100%; margin-top:40px;}
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
      count : []
    };
  },
  components: {},
  methods: {
    countUp(index){
      this.count[index] += 1;
    }
  },
  mounted() {
   
  },
  created() {
    this.products.forEach(()=> this.count.push(0));
  },
};
</script>
