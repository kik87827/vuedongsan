<template>
  <!--  <img :src="item.image" class="room-img" alt="" />
    <h4 @click="modalOpen(index)">{{ item.title }}</h4>
    <p>{{ item.price }} 원</p>
    <div>
      <button @click="countUp(index)">허위매물신고</button> <span>신고수 : {{ count[index] }}</span>
    </div> -->
  <div>
    <img :src="roomData.image" class="room-img" alt="" />
    <h4 @click="sendModalOpen()">{{ roomData.title }}</h4>
    <p>{{ roomData.price }} 원</p>
    <div>
      <button @click="sendCountUp()">허위매물신고</button> <span>신고수 : {{ countItem }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductItem",
  props: {
    countItem: Number,
    roomData: Object,
  },
  emits: ["sendCountUp", "sendModalOpen"],
  methods: {
    sendModalOpen() {
      this.$emit("sendModalOpen", this.roomData.id);
    },
    sendCountUp() {
      this.$emit("sendCountUp");
    },
  },
};
</script>

<style scoped></style>
