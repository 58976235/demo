<template>
  <div
    v-show="isShow"
    class="bullet-box"
    :style="{
      width: widthStr,
      left: leftStr,
      top: topStr,
    }"
  >
    <div v-for="bullet in bulletRow" :key="bullet" class="bullet"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      topStr: "",
      leftStr: "",
      topNum: 0,
      isShow:false
    };
  },
  props: {
    width: {
      type: Number,
    },
    bulletRow: {
      type: Number,
    },
    top: {
      type: Number,
    },
    left: {
      type: Number,
    },
    time:{
      type:Number
    }
  },
  computed: {
    widthStr() {
      return this.width + "px";
    },
  },
  mounted() {
    this.topStr = this.top + "px";
    this.leftStr = this.left + "px";
    this.topNum = this.top;
    setTimeout(() => {
      setInterval(() => {
        this.isShow=true
        if (this.topNum > -100) {
          this.topNum -= 2;
          this.topStr = this.topNum + "px";
        } else {
          this.topNum= this.top;
          this.leftStr = this.left + "px";
          this.topStr = this.top + "px";
        }
      }, 6);
    }, this.time*60);
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