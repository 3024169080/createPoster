<template>
  <div class="home">
    <div class="box">
      <div class="mousePosition">
        <div>
          <h5>鼠标位置</h5>
          <p>{{mouseP.mouseX}}X,{{mouseP.mouseY}}Y</p>
        </div>
      </div>
      <div class="content" ref="content">
        <div class="img1" ref="img1" @mousedown="toDown" @mouseup="toup">
          <img src="https://c-ssl.duitang.com/uploads/item/201509/30/20150930140213_ZCFSr.jpeg" alt />
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: "",
  data() {
    return {
      // 鼠标位置
      mouseP: {
        mouseX: 0,
        mouseY: 0
      },
      moveP: {
        width: 0,
        height: 0,
        offsetX: 0,
        offsetY: 0
      },
      contentP: {
        width: 0,
        height: 0,
        offsetX: 0,
        offsetY: 0
      },
      // 鼠标移动属性
      moveObj: {}
    };
  },
  components: {},
  computed: {},
  created() {},
  mounted() {
    this.init();
  },
  methods: {
    init() {
      window.onmousemove = e => {
        // console.log(e);
        this.moveObj = e;
        this.mouseP = {
          mouseX: e.x,
          mouseY: e.y
        };
        // this.elementMove();
      };
      this.contentP = {
        width: this.$refs.content.offsetWidth,
        height: this.$refs.content.offsetHeight,
        offsetX: this.$refs.content.offsetLeft,
        offsetY: this.$refs.content.offsetTop
      };
      this.moveP = {
        width: this.$refs.img1.offsetWidth,
        height: this.$refs.img1.offsetHeight,
        offsetX: this.$refs.img1.offsetLeft,
        offsetY: this.$refs.img1.offsetTop
      };
    },
    elementMove() {
      let moveX =
        this.mouseP.mouseX - this.contentP.offsetX - this.moveP.width / 2;
      let moveY =
        this.mouseP.mouseY - this.contentP.offsetY - this.moveP.height / 2;
      // 不超左边
      if (this.mouseP.mouseX - this.moveP.width / 2 <= this.contentP.offsetX) {
        moveX = 0;
      }
      // 不超右边
      if (
        this.mouseP.mouseX + this.moveP.width / 2 >=
        this.contentP.offsetX + this.contentP.width
      ) {
        moveX = this.contentP.width - this.moveP.width;
      }
      // 不超上边
      if (this.mouseP.mouseY - this.moveP.height / 2 <= this.contentP.offsetY) {
        moveY = 0;
      }
      // 不超下边
      if (
        this.mouseP.mouseY + this.moveP.height / 2 >=
        this.contentP.offsetY + this.contentP.height
      ) {
        moveY = this.contentP.height - this.moveP.height;
      }
      this.$refs.img1.style.left = moveX + "px";
      this.$refs.img1.style.top = moveY + "px";
    },
    toDown() {
      document.onmousemove = e => {
        e.preventDefault(); // 阻止默认事件
        this.elementMove();
      };
      document.onmouseup = e => {
        document.onmousemove = null;
        document.onmouseup = null;
      };
    },
    toup() {}
  }
};
</script>

<style lang="scss" scoped>
.home {
  // box-sizing: border-box;
}
ul,
.li {
  list-style: none;
}
.box {
  margin: 0 auto;
  margin-top: 100px;
  width: 600px;
  height: 400px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.mousePosition {
  width: 100px;
  border: 1px solid #333;
}
.content {
  width: 400px;
  height: 400px;
  position: relative;
  // border: 1px solid #000;
  background: #e5e5e5;
  margin: 0 auto;
  .img1 {
    top: 0;
    left: 0;
    position: absolute;
    width: 100px;
    height: 100px;
    img {
      width: 100%;
    }
  }
}
</style>
