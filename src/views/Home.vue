<template>
  <div class="home">
    <div class="mousePosition">
      <p>鼠标位置:{{mouseP.mouseX}}X,{{mouseP.mouseY}}Y</p>
    </div>
    <div class="content">
      <img class="img1" ref="img1" src="https://c-ssl.duitang.com/uploads/item/201509/30/20150930140213_ZCFSr.jpeg" alt="">
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
        console.log(e);
        this.moveObj = e;
        this.mouseP = {
          mouseX: e.x,
          mouseY: e.y
        };
        this.elementMove();
      };
    },
    elementMove(){
      this.$refs.img1.style.left=this.mouseP.mouseX+'px';
      this.$refs.img1.style.top=this.mouseP.mouseY+'px';
    },
  }
};
</script>

<style lang="scss" scoped>
.content{
  width: 400px;
  height: 400px;
  position: relative;
  border: 1px solid #000;
  margin: 0 auto;
  .img1{
    top: 0;
    left: 0;
    position: fixed;
    width: 100px;
    height: 100px;
  }
}
</style>
