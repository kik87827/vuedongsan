<template>
  <div class="black-bg">
    <div class="white-bg">
      <img :src="roomData[modalIndex].image" class="room-img" alt="" />
      <h4>{{ roomData[modalIndex].title }}</h4>
      <p>{{ roomData[modalIndex].content }}</p>
      <p>{{ roomData[modalIndex].price }} 원</p>
      <div>
        <input v-model.number="month" maxlength="2" />
        <!-- <input type="number" v-model="month" /> -->
        <!-- <textarea v-model="month"></textarea> -->
        <!-- <select v-model="month">
          <option>1</option>
          <option>10</option>
          <option>20</option>
        </select> -->
      </div>
      <div style="color: red">{{ warnText }}</div>
      <br />
      <p>{{ month }}개월 선택함 : {{ roomData[modalIndex].price * month }} 원</p>
      <br />
      <div><button @click="emitModal">닫기</button></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      month: 1,
      warnText: "",
    };
  },
  watch: {
    month(currentValue, beforeValue) {
      if (currentValue.length === 0) {
        this.warnText = "";
        return;
      }
      if (typeof currentValue !== "number") {
        this.warnText = "숫자만입력";
        this.month = 1;
      } else {
        this.warnText = "";
      }
      if (currentValue > 12) {
        this.warnText = "12개월 이내";
      } else if (currentValue === 0) {
        this.warnText = "1개월 이상";
      }
    },
  },
  props: {
    modalToggle: Boolean,
    roomData: Array,
    modalIndex: Number,
  },
  emits: ["modalClose"],
  methods: {
    emitModal() {
      this.$emit("modalClose", false);
    },
    resetValue() {
      this.month = 1;
    },
  },
  components: {},
};
</script>

<style scoped></style>
