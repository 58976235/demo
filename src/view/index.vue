<template>
  <div
    class="box"
    @mousedown="onMouseDown"
    @mousemove="onMouseMove"
    @mouseup="onMouseUp"
  >
    <div ref="game" class="game-box game" :style="{backgroundPositionY:backgroundPositionY+'px'}">
      <Me
        ref="me"
        @touchmove="onTouchMove"
        :left="me.pageX"
        :top="me.pageY"
        :width="me.meWidth"
        :height="me.meHeight"
      />
      <my-bullet
        v-for="bullet in myBullet.bulletList"
        :key="bullet"
        :time='bullet'
        :left="me.pageX"
        :top="me.pageY"
        :width="me.meWidth"
        :bulletRow='myBullet.bulletRow'
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
      backgroundPositionY:0,
      me:{
        pageX: 156,
        pageY: 610,
        meWidth: 102,
        meHeight: 126,
      },
      myBullet:{
        bulletRow:2,
        bulletList: 36,
      }
    };
  },
  components: {
    Me,
    MyBullet,
  },
  methods: {
    onTouchMove(ev) {
      if (
        ev.touches[0].pageX - this.me.meWidth / 2 > 0 &&
        ev.touches[0].pageX + this.me.meWidth / 2 < ev.view.outerWidth
      ) {
        this.me.pageX = ev.touches[0].pageX - this.me.meWidth / 2;
      }
      if (
        ev.touches[0].pageY + this.me.meHeight / 2 < ev.view.outerHeight &&
        ev.touches[0].pageY - this.me.meHeight / 2 > 0
      ) {
        this.me.pageY = ev.touches[0].pageY - this.me.meHeight / 2;
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
        let left = ev.pageX - this.$refs.game.offsetLeft - this.me.meWidth / 2;
        let width = this.me.meWidth;
        let height = this.me.meHeight / 2;
        let top = ev.pageY - this.me.meHeight / 2;
        let right = this.$refs.game.clientWidth;
        let bottom = this.$refs.game.clientHeight;
        if (left > 0 && left + width < right) {
          this.me.pageX = left;
        }
        if (top > 0 && top + 2 * height < bottom) {
          this.me.pageY = top;
        }
      }
    },
  },
  mounted() {
    /* let num; */
    setInterval(() => {
      this.backgroundPositionY++
      /* num = Symbol("id");
      if (this.myBullet.bulletList.length > 55) {
        this.myBullet.bulletList.shift();
      }
      this.myBullet.bulletList.push(num); */
    }, 60);
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