<template>
  <!--  <div class="black-bg" v-if="modalToggle">
    <div class="white-bg">
      <img :src="`/room${modalIndex}.jpg`" class="room-img" alt="" />
      <h4>{{ roomData[modalIndex].title }}</h4>
      <p>{{ roomData[modalIndex].content }}</p>
      <p>{{ roomData[modalIndex].price }} 원</p>
      <DiscountBanner />
      <div><button @click="modalToggle = false">닫기</button></div>
    </div>
  </div> -->

  <!-- <div class="start" :class="{ end : modalToggle }">
    <Modal :roomData="roomData" :modalIndex="modalIndex" @modalClose="handleClose" v-if="modalToggle" />
  </div> -->
  <transition name="fade">
    <Modal :roomData="roomData" :modalIndex="modalIndex" @modalClose="handleClose" v-if="modalToggle" />
  </transition>

  <div class="menu">
    <a v-for="(item, index) in menus" :key="item">{{ item }}</a>
  </div>

  <DiscountBanner v-if="bannerToggle" />
  <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->

  <div style="text-align:center">
    <button @click="priceSort">가격순정렬</button>
    <button @click="priceReverseSort">가격역순정렬</button>
    <button @click="titleSort">가나다정렬</button>
    <button @click="originSort">원래대로</button>
  </div>

  <div class="room-list">
    <ProductItem
      v-for="(item, index) in roomData"
      :key="item.id"
      :roomData="item"
      :countItem="count[index]"
      @sendCountUp="countUp(index)"
      @sendModalOpen="modalOpen($event)"
    />
    <!-- <img :src="item.image" class="room-img" alt="" />
    <h4 @click="modalOpen(index)">{{ item.title }}</h4>
    <p>{{ item.price }} 원</p>
    <div>
      <button @click="countUp(index)">허위매물신고</button> <span>신고수 : {{ count[index] }}</span>
    </div> -->
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
.white-bg .room-img {
  margin-top: 0;
}

.discount {
  background: #eee;
  text-align: center;
  padding: 20px;
  margin: 10px;
  display: block;
}

.start{opacity:0; transition: all 1s;}
.end{opacity:1;}

.fade-enter-from{opacity:0;}
.fade-enter-active{transition: all 1s;}
.fade-enter-to{opacity:1;}

.fade-leave-from{opacity:1;}
.fade-leave-active{transition: all 1s;}
.fade-leave-to{opacity:0;}
</style>

<script>
import roomData from "./assets/data";
import DiscountBanner from "./components/DiscountBanner.vue";
import Modal from "./components/Modal.vue";
import ProductItem from "./components/ProductItem.vue";

export default {
  name: "App",
  data() {
    return {
      /* price1: 60,
      price2: 70,
      style: "color : red",
      products: [
        { title: "역삼동원룸", price: "50만원" },
        { title: "천호동원룸", price: "가격은아무거나" },
        { title: "마포구원룸", price: "가격은아무거나" },
      ], */
      bannerToggle : true,
      //bannerTime : 0,
      menus: ["Home", "Products", "About"],
      count: [],
      modalToggle: false,
      modalIndex: 0,
      roomData,
      roomDataOrigin : [...roomData],
    };
  },
  components: {
    DiscountBanner,
    ProductItem,
    Modal,
  },
  methods: {
    countUp(index) {
      this.count[index] += 1;
    },
    modalOpen(num) {
      this.modalToggle = true;
      this.modalIndex = num;
    },
    handleClose() {
      this.modalToggle = false;
    },
    priceSort(){
      this.roomData.sort((a,b)=>{
        return a.price - b.price;
      });
    },
    priceReverseSort(){
      this.roomData.sort((a,b)=>{
        return b.price - a.price;
      });
    },
    titleSort(){
      this.roomData.sort((a, b) => a.title.localeCompare(b.title, { sensitivity: 'base' }));
    },
    originSort(){
      this.roomData = [...this.roomDataOrigin];
    }
  },
  mounted() {
   /*  this.bannerTime = setTimeout(() => {
      this.bannerToggle = false;
    }, 2000); */
  },
  unmounted() {
    /* clearTimeout(this.bannerTime);
    this.bannerTime = 0; */
  },
  created() {
    //this.roomData.forEach(() => this.count.push(0));
    this.count = new Array(this.roomData.length).fill(0);
  },
};
</script>
