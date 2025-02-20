<template>
  <div class="black-bg">
    <div class="white-bg">
      <img :src="roomData[modalIndex].image" class="room-img" alt="" />
      <h4>{{ roomData[modalIndex].title }}</h4>
      <p>{{ roomData[modalIndex].content }}</p>
      <p>{{ roomData[modalIndex].price }} 원</p>
      <div><button @click="emitModal">닫기</button></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: {
    modalToggle: Boolean,
    roomData: Array,
    modalIndex: Number,
  },
  methods: {
    emitModal() {
      this.$emit("modalClose", false);
    },
  },
  components: {},
};
</script>

<style scoped></style>
