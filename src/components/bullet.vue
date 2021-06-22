<template>
  <div
      class="bullet-box"
      :style="{
        width: widthStr,
        left: leftStr,
        top: topStr
      }"
    >
      <div v-for="bullet in bulletNum" :key='bullet' class="bullet"></div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      topStr: "",
      leftStr: "",
      bulletNum:4,
      bulletList:[0]
    };
  },
  props: {
    width: {
      type: Number,
    },
    top: {
      type: Number,
    },
    left: {
      type: Number,
    },
  },
  computed: {
    widthStr() {
      return this.width + "px";
    }
  },
  mounted() {
    this.leftStr = this.left + "px";
    this.topNum = this.top;
    setInterval(() => {
      this.topNum -=1;
      this.topStr = this.topNum + "px";
    }, 6); 
   
  },
};
</script>

<style lang="scss" scoped>
.bullet-box {
  display: flex;
  justify-content: space-around;
  align-items: flex-start;
  position: absolute;
  .bullet {
    width: 5px;
    height: 11px;
    background: url("../assets/images/bullet1.png") no-repeat;
  }
}
</style>