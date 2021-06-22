<template>
  <div
    class="box"
    @mousedown="onMouseDown"
    @mousemove="onMouseMove"
    @mouseup="onMouseUp"
  >
    <div ref="game" class="game-box game">
      <Me
        ref="me"
        @touchmove="onTouchMove"
        :left="pageX"
        :top="pageY"
        :width="meWidth"
        :height="meHeight"
      />
      <my-bullet
        v-for="bullet in bulletList"
        :key="bullet"
        :left="pageX"
        :top="pageY"
        :width="meWidth"
      />
    </div>
  </div>
</template>

<script>
import Me from "../components/me.vue";
import MyBullet from "../components/bullet.vue";
export default {
  data() {
    return {
      isMouseDown: false,
      pageX: 156,
      pageY: 610,
      meWidth: 102,
      meHeight: 126,
      bulletList: [0],
    };
  },
  components: {
    Me,
    MyBullet,
  },
  methods: {
    onTouchMove(ev) {
      if (
        ev.touches[0].pageX - this.meWidth / 2 > 0 &&
        ev.touches[0].pageX + this.meWidth / 2 < ev.view.outerWidth
      ) {
        this.pageX = ev.touches[0].pageX - this.meWidth / 2;
      }
      if (
        ev.touches[0].pageY + this.meHeight / 2 < ev.view.outerHeight &&
        ev.touches[0].pageY - this.meHeight / 2 > 0
      ) {
        this.pageY = ev.touches[0].pageY - this.meHeight / 2;
      }
    },
    onMouseDown(ev) {
      if (ev.target.className == "me-box") {
        this.isMouseDown = true;
      }
    },
    onMouseUp() {
      this.isMouseDown = false;
    },
    onMouseMove(ev) {
      if (this.isMouseDown) {
        let left = ev.pageX - this.$refs.game.offsetLeft - this.meWidth / 2;
        let width = this.meWidth;
        let height = this.meHeight / 2;
        let top = ev.pageY - this.meHeight / 2;
        let right = this.$refs.game.clientWidth;
        let bottom = this.$refs.game.clientHeight;
        if (left > 0 && left + width < right) {
          this.pageX = left;
        }
        if (top > 0 && top + 2 * height < bottom) {
          this.pageY = top;
        }
      }
    },
  },
  mounted() {
    let num;
    setInterval(() => {
      num = Symbol("id");
      if (this.bulletList.length > 35) {
        this.bulletList.shift();
      }
      this.bulletList.push(num);
    }, 120);
  },
};
</script>

<style scoped>
.box {
  width: 100%;
  height: 100%;
}
.game {
  position: relative;
  margin: 0 auto;
  background: url("../assets/images/background.png");
}
.game-box {
  width: 414px;
  height: 736px;
}
@media screen and (max-width: 1024) {
  .game-box {
    touch-action: none;
    width: 100vw;
    height: 100vh;
  }
}
</style>