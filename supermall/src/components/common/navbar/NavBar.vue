<template>
  <div class="navbar">
    <div class="left"><slot name="left"></slot></div>
    <div class="center"><slot name="center"></slot></div>
    <div class="right"><slot name="right"></slot></div>
  </div>
</template>

<script>
export default {
  name: 'NavBar',
  data() { 
    return {

    }
  },
  props: {

  },
  components:{
  },
  mounted() {

  },
  methods:{

  },
  beforeCreate() {}, //生命周期 - 创建之前
  beforeMount() {}, //生命周期 - 挂载之前
  beforeUpdate() {}, //生命周期 - 更新之前
  updated() {}, //生命周期 - 更新之后
  beforeDestroy() {}, //生命周期 - 销毁之前
  destroyed() {}, //生命周期 - 销毁完成
  activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
 }
</script>

<style scoped>
.navbar {
  display: flex;
  height: 44px;
  text-align: center;
  line-height: 44px;
  box-shadow: 0, 1px, 1px, rgba(100, 100, 100, .1)
}

.left, .right {
  width: 60px;
}
.center {
  flex: 1;
}
</style>